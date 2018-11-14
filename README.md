	轻量级caffe前向推理框架

	本项目为对happynear版本的caffe进行精简化:
	1、去除冗余依赖boost、hdf5、lmdb、levedb等，简化以后caffe前向框架更加小型化，并且保持了原生caffe调用习惯（相比于mini-caffe）
	2、去除训练用到的loss计算以及solver源码
	3、调整修改内存管理机制（去除boost）

	小赞：
		相比于mini-caffe，该精简化版本的caffe更加原生态，函数调用和原版的caffe没有区别，同时也支持mkl编译，多GPU模式编译（nccl)
		提供的cmake可以在ubuntu下编译，同时也可以在windows下编译使用。

	注意：
		windows下编译，blob.hpp、io.hpp、net.hpp、common.hpp、layer.hpp、caffe.pb.h的文件开始加入：
	1、编译时：
			#define LIBCAFFE __declspec(dllexport)
	2、调用时：
			#ifdef CAFFE_EXPORTS
			#define LIBCAFFE __declspec(dllexport)
			#else
			#define LIBCAFFE __declspec(dllimport)
			#endif
			
	这是一个坑，一开始编译时加入第二种宏定义方式，总是报错。最后不得已使用这种方式。ubuntu下不存在这些问题！

	如果需要添加新的层，需要重新生成caffe.pb.h和caffe.pb.cc，protobuf库自由选择，但是版本一定要一致。
