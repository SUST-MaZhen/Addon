# 工程名 
SET( TARGETFILENAME "addon" )
PROJECT( ${TARGETFILENAME} ) 

# CMake 最低版本设置
cmake_minimum_required(VERSION 3.8)
   
# node library 
SET(NODE_LIBRARIES node.lib) 
SET(NODE_LIBRARY_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/thirdPart/node/lib )
 
# node library setting
IF (WIN32)
	FIND_LIBRARY(NODE_LIBRARY 
		NAMES  node 
		PATHS  ${CMAKE_CURRENT_SOURCE_DIR}/thirdPart/node/lib
	)
ENDIF (WIN32)
                         
# - 设置包含目录
INCLUDE_DIRECTORIES(
    ${CMAKE_CURRENT_SOURCE_DIR}/thirdPart/node/include/node 
)                         

SET( src demo.cc)

# 设置库文件目录
# 确保在生成目标之前
# windows上执行语句
IF (WIN32)
	LINK_DIRECTORIES( ${NODE_LIBRARY_DIRS} )
ENDIF (WIN32)

# 生成可执行文件
#add_executable(${TARGETFILENAME} demo.cpp)

# 生成静态库
#ADD_LIBRARY(${TARGETFILENAME} STATIC demo.cpp) 

# 生成动态库或共享库
ADD_LIBRARY ( ${TARGETFILENAME} SHARED 
     ${src}
)

# 修改后缀名为  .node    
SET_TARGET_PROPERTIES(${TARGETFILENAME} PROPERTIES SUFFIX ".node")

# 设置链接库文件
# windows上执行语句
IF (WIN32)
	TARGET_LINK_LIBRARIES( ${TARGETFILENAME}
		${NODE_LIBRARIES}  
	)
ENDIF (WIN32)