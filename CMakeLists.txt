cmake_minimum_required(VERSION 3.25)
project(TransformerEngine CXX CUDA)

set(CMAKE_CUDA_STANDARD 17)

set(CMAKE_CUDA_ARCHITECTURES "80")

add_subdirectory(transformer_engine/common)

add_library(transformer_engine_torch SHARED
        transformer_engine/pytorch/csrc/common.cu
        transformer_engine/pytorch/csrc/ts_fp8_op.cpp
        transformer_engine/pytorch/csrc/userbuffers/ipcsocket.cc
        transformer_engine/pytorch/csrc/userbuffers/userbuffers-host.cpp
        transformer_engine/pytorch/csrc/userbuffers/userbuffers.cu
        transformer_engine/pytorch/csrc/extensions/activation.cu
        transformer_engine/pytorch/csrc/extensions/apply_rope.cu
        transformer_engine/pytorch/csrc/extensions/attention.cu
        transformer_engine/pytorch/csrc/extensions/cast.cu
        transformer_engine/pytorch/csrc/extensions/gemm.cu
        transformer_engine/pytorch/csrc/extensions/misc.cu
        transformer_engine/pytorch/csrc/extensions/normalization.cu
        transformer_engine/pytorch/csrc/extensions/permutation.cu
        transformer_engine/pytorch/csrc/extensions/pybind.cpp
        transformer_engine/pytorch/csrc/extensions/recipe.cu
        transformer_engine/pytorch/csrc/extensions/softmax.cu
        transformer_engine/pytorch/csrc/extensions/transpose.cu
        transformer_engine/pytorch/csrc/extensions/multi_tensor/multi_tensor_adam.cu
        transformer_engine/pytorch/csrc/extensions/multi_tensor/multi_tensor_l2norm_kernel.cu
        transformer_engine/pytorch/csrc/extensions/multi_tensor/multi_tensor_scale_kernel.cu
        transformer_engine/pytorch/csrc/extensions/multi_tensor/multi_tensor_sgd_kernel.cu)

target_include_directories(transformer_engine_torch PRIVATE
        transformer_engine/
        transformer_engine/common
        transformer_engine/common/include
        transformer_engine/pytorch/csrc
        /usr/local/lib/python3.6/dist-packages/torch/include
        /usr/local/lib/python3.6/dist-packages/torch/include/torch/csrc/api/include
        /usr/local/lib/python3.6/dist-packages/torch/include/TH
        /usr/local/lib/python3.6/dist-packages/torch/include/THC
        ${CMAKE_CUDA_TOOLKIT_INCLUDE_DIRECTORIES}
        )