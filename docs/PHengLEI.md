# PHengLEI 风雷软件使用教程

## 1、 文件构成

 * 参数文件夹bin  

    * 总控文件key.hypara——控制求解器执行的任务类型，如网格转换、网格分区以及CFD计算

      ```c++
      //屏幕输出的文件名
      string title = "PHengLEI Main Parameter Control File";
      
      // IMPORTANT NOTICE: DON NOT MODIFY THE FOWLLOWING LINE.
      //默认参数文件，通常不做任何修改
      string defaultParaFile = "./bin/cfd_para.hypara";
      
      // ndim: Dimensional of the grid, 2 or 3.
      // nparafile: the number of parameter files.
      // nsimutask: simulation task type.
      //            0 -- CFD Solver of NS or Turbulation.
      //            1 -- Grid generation: for special typical cases, such as cylinder, flat plate, etc.
      //                 Grid conversion: from other format to PHengLEI format (.fts).
      //                 Grid reconstruction: such as grid adaptation.
      //                 Grid merging: merge two blocks into one block.
      //                 Grid repairing: repair the original grid in order to remove the negative volume cells.
      //            2 -- Wall distance computation for turb-solver.
      //            3 -- Grid partition.
      //            4 -- Knowledge repository / examples of PHengLEI-API.
      //计算网格维数:2维或3维
      int ndim      = 2;
      
      //参数文件数目
      int nparafile = 1;
      
      //任务类型 0:数值计算;1:网格操作 ;2:壁面距离计算 ; 3:网格分区
      int    nsimutask    = 0;
      
      //string parafilename = "./bin/cfd_para_subsonic.hypara";
      
      //与任务类型相匹配的参数文件名
      string parafilename = "./bin/cfd_para_transonic.hypara";
      
      //string parafilename = "./bin/cfd_para_supersonic.hypara";
      //string parafilename = "./bin/cfd_para_hypersonic.hypara";
      //string parafilename = "./bin/incompressible.hypara";
      
      //int    nsimutask    = 1;
      //string parafilename = "./bin/grid_para.hypara";
      
      //int    nsimutask    = 2;
      //string parafilename = "./bin/cfd_para.hypara";
      
      //int    nsimutask    = 3;
      //string parafilename = "./bin/partition.hypara";
      
      //int    nsimutask    = 4;
      //string parafilename = "./bin/repository.hypara";
      
      //int    nsimutask    = 5;
      //string parafilename = "./bin/overset_grid_view.hypara";
      
      //int    nsimutask    = 14;
      //string parafilename = "./bin/integrative_solver.hypara";
      
      //int    nsimutask    = 99;
      //string parafilename = "./bin/post_processing.hypara";
      
      // ---------------- Advanced Parameters, DO NOT care it ----------------
      int numberOfGridProcessor = 0;
      // ATP read
      //@string parafilename1 = ""
      //@string parafilename2 = "";
      
      ```

    * 网格控制文件grid_para.hypara——控制网格格式转换、修复、重构以及合并等操作

      ```c++
      #########################################################################
      #                           Grid data type                              #
      #########################################################################
      // gridtype: Grid type for generation, conversion, reconstruction, merging.
      //           0 -- Unstructured grid.
      //           1 -- Structured grid.
      // axisup:   Type of Cartisien coordinates system, used in grid conversion.
      //           1 -- Y upward. (default)
      //           2 -- Z upward.
      // from_gtype: Type of grid data type in grid conversion process.
      //            -1 -- MULTI_TYPE.
      //             1 -- PHengLEI, *.fts.
      //             2 -- CGNS, *.cgns.
      //             3 -- Plot3D type of structured grid, *.dat/*.grd.
      //             4 -- Fieldview type of unstructured grid, *.dat/*.inp.
      //             5 -- Fluent, *.cas/*.msh.
      //             6 -- Ustar, mgrid.in.
      //             7 -- Hybrid, include both of unstructured and structured grid, *.fts.
      //             8 -- GMSH, *.msh.
      
      // 网格类型: 0:非结构 1:结构 2:混合
      int gridtype   = 0;
      
      //Cartesian坐标系类型 1:y轴向上 2:Z轴向上
      int axisup     = 1;
      
      //读入的网格类型 -1:混合网格 1:PHengLEI格式 2:CGNS 格式 3:结构网格Gridgen/Plot3D格式 4:非结构网格 FieldView格式 5:FLUENT格式 6:Ustar格式 7:Mixed Grid 8:GMESH格式
      int from_gtype = 2;
      
      #########################################################################
      #                           File path                                   #
      #########################################################################
      // from_gfile: path of original data file for unstructure grid convert from.
      // out_gfile:  path of target file for grid convert to, *.fts type of file usually.
      
      // 输入的文件路径及文件名
      string from_gfile = "./grid/rae2822_hybrid2d.cgns";
      
      //输出的文件路径及文件名
      string out_gfile  = "./grid/rae2822_hybrid2d.fts";
      ```

    *  网格分区文件partition.hypara——当总控文件中选择网格操作 即nsimutask=3时，通过修改分区文件参数，就可以进行网格分区

      ```c++
      // pgridtype: The grid type. 
      //            0 -- unstruct grid.
      //            1 -- struct grid.
      // maxproc:   The number of partition zones that want to be divided into,
      //            which is equal to the number of CPU processors you want.
      //            Usually, 50~100 thousands structured cells per CPU-Core is suggested.
      //            30~70  thousands unstructured cells per CPU-Core is suggested.
      // original_grid_file:  Original grid file that want to be divided(PHengLEI type, *.fts).
      // partition_grid_file: Target partition grid file(PHengLEI type, *.fts).
      
      //网格类型 0:非结构网格 1:结构网格 2:加密网格
      int pgridtype = 0;
      
      //网格分区数(最大进程数)
      int maxproc   = 4;
      
      //分区前网格文件路径和文件名
      string original_grid_file  = "./grid/rae2822_hybrid2d.fts";
      
      //分区后网格文件路径和文件名
      string partition_grid_file = "./grid/rae2822_hybrid2d__4.fts";
      
      // numberOfMultigrid: Number of multi-grid levels, ONLY used for structured grid.
      //                    1 -- single level.
      //                    2 -- 2 level. 
      //                    N -- N level,..., et al.
      //多重网格计算重数(只针对结构网格)
      int numberOfMultigrid = 1;
      
      ```

      * 解算器默认文件cfd_para.hypara:包含了所有的参数(网 格转换、分区、cfd计算)，程序执行任何操作修改相应文件中的参数即可覆盖cfd_para.hypara中 相同参数值，默认参数文件除特殊情况一般不允许修改。
      * 亚声速流动参数文件cfd_para_subsonic.hypara:包含了亚声速流动计算推荐的参数，计算时只要修改相应参数即可覆盖cfd_para.hypara中相同参数值。
      *  跨声速流动参数文件cfd_para_transonic.hypara:包含了跨声速流动计算推荐的参数，计算时只要修改相应参数即可覆盖cfd_para.hypara中相同参数值。 
      * 超声速流动参数文件cfd_para_supersonic.hypara:包含了超声速流动计算推荐的参数，计算时只要修改相应参数即可覆盖cfd_para.hypara中相同参数值。
      *  高超声速流动参数文件cfd_para_hypersonic.hypara:包含了高超声速流动计算推荐的参数，计算时只要修改相应参数即可覆盖cfd_para.hypara中相同参数值。

 * 网格文件夹grid——所有网格数据文件，包括转换后的网格文件和分区后的网格文件

 * 结果文件夹results

   <p align="center">
     <img src="./images/result.png" />
   </p>
   ## 2、使用步骤
   
   <p align="center">
     <img src="./images/process.png" />
   </p>
   
   
   
   
   

