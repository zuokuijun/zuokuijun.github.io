# PCA——主成分分析



* PCA寻找尽可能体现数据之间差异的属性
* PCA寻找能够尽可能重建原本属性

  [通俗易懂的讲解什么是PCA？——主成分分析](https://www.zhihu.com/question/41120789/answer/474222214)

```python
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% Matlab code to produce PCA animations shown here:
% http://stats.stackexchange.com/questions/2691
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

% Static image

clear all
rng(42)

X = randn(100,2);
X = X*chol([1 0.6; 0.6 0.6]);
X = bsxfun(@minus, X, mean(X));

[a,b] = eig(cov(X));

fig = figure('Position', [100 100 1000 400]);
set(gcf,'color','w');
axis([-3.5 3.5 -3.5 3.5])
axis square
hold on
scatter(X(:,1), X(:,2), 'b', 'filled')

%% Rotating animation

fig = figure('Position', [100 100 1000 400]);
set(gcf,'color','w');
axis([-3.5 3.5 -3.5 3.5])
axis square
hold on

for alpha = 1:1:179
    w = [cosd(alpha) sind(alpha)];
    z = X*w'*w;
    
    cla
    for i=1:100
        plot([X(i,1) z(i,1)], [X(i,2) z(i,2)], 'r')
    end
    
    plot(w(1)*3.5*[-1 1], w(2)*3.5*[-1 1], 'k')
    plot(-w(2)*2*[-1 1], w(1)*2*[-1 1], 'Color', [.6 .6 .6])
    
    scatter(z(:,1), z(:,2), 'r', 'filled')
    scatter(X(:,1), X(:,2), 'b', 'filled')
    scatter(0,0,65,'k','filled', 'LineWidth', 2, 'MarkerFaceColor', [1 1 1], 'MarkerEdgeColor', [0 0 0])
    
    a1 = 3.5;
    a2 = 4.5;
    plot(a(1,2)*[-a2 -a1], a(2,2)*[-a2 -a1], 'm', 'LineWidth', 2)
    plot(a(1,2)*[ a1  a2], a(2,2)*[ a1  a2], 'm', 'LineWidth', 2)
    drawnow
    
    frame = getframe(fig);
    if alpha == 1
        [imind,map] = rgb2ind(frame.cdata,16,'nodither');
    else
        imind(:,:,1,alpha) = rgb2ind(frame.cdata,map,'nodither');
    end
end
imwrite(imind,map, 'animation_pca.gif', 'DelayTime', 0, 'LoopCount', inf)

%% Pendulum animation

fig = figure('Position', [100 100 1000 400]);
set(gcf,'color','w');
axis([-3.5 3.5 -3.5 3.5])
axis square
hold on

alpha = -45;
omega = 0;
for t = 1:1:1000
    w = [cosd(alpha) sind(alpha)];
    z = X*w'*w;
    
    M = sum(sum((z * [0 1; -1 0]) .* (X-z), 2));
    omega = omega + M;
    omega = omega * 0.93;
    alpha = alpha + omega/40;
    if(abs(omega)<1 && abs(alpha-abs(atand(a(2,2)/a(1,2)))) < 1)
        break
    end
    
    cla
    for i=1:100
        plot([X(i,1) z(i,1)], [X(i,2) z(i,2)], 'r')
    end
    
    plot(w(1)*3.5*[-1 1], w(2)*3.5*[-1 1], 'k')
    plot(-w(2)*2*[-1 1], w(1)*2*[-1 1], 'Color', [.6 .6 .6])
    
    scatter(z(:,1), z(:,2), 'r', 'filled')
    scatter(X(:,1), X(:,2), 'b', 'filled')
    scatter(0,0,65,'k','filled', 'LineWidth', 2, 'MarkerFaceColor', [1 1 1], 'MarkerEdgeColor', [0 0 0])
    
    a1 = 3.5;
    a2 = 4.5;
    plot(a(1,2)*[-a2 -a1], a(2,2)*[-a2 -a1], 'm', 'LineWidth', 2)
    plot(a(1,2)*[ a1  a2], a(2,2)*[ a1  a2], 'm', 'LineWidth', 2)
    
    pause(0.01)
    
    drawnow
    
    frame = getframe(fig);
    if t == 1
        [imind,map] = rgb2ind(frame.cdata,16,'nodither');
    else
        imind(:,:,1,t) = rgb2ind(frame.cdata,map,'nodither');
    end
end
imwrite(imind,map, 'animation_pca_pendulum.gif', 'DelayTime', 0, 'LoopCount', inf)
```
