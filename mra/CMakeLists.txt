include(AddTTGExecutable)

add_ttg_executable(tensortest tests/tensor_test.cc)
add_ttg_executable(mra-device-host
                   mra-ttg-device.cc
                   gl.cc
                   mra-ttg-device.cc
                   kernels.cc
                   mratwoscale.cc
                   COMPILE_DEFINITIONS TTG_ENABLE_HOST=1
                   LINK_LIBRARIES MADworld
                   RUNTIMES "parsec")

add_ttg_executable(mra-device-host
                   mra-ttg-device.cc
                   gl.cc
                   mra-ttg-device.cc
                   kernels.cc
                   mratwoscale.cc
                   COMPILE_DEFINITIONS TTG_ENABLE_HOST=1
                   LINK_LIBRARIES MADworld
                   RUNTIMES "mad")

if (TTG_HAVE_CUDA)
  add_ttg_executable(mradevice-cuda
                     mra-ttg-device.cc
                     gl.cc
                     mra-ttg-device.cc
                     kernels.cu
                     mratwoscale.cc
                     COMPILE_DEFINITIONS TTG_ENABLE_CUDA=1
                     COMPILE_OPTIONS $<$<COMPILE_LANGUAGE:CUDA>:--expt-relaxed-constexpr>
                     LINK_LIBRARIES MADworld
                     RUNTIMES "parsec")
endif (TTG_HAVE_CUDA)
