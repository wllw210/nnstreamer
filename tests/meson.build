subdir('nnstreamer_tensors/tensors_test')

gtest_dep = dependency('gtest', main: false, required: true)

if gtest_dep.found()
  # This custom filter is used in unittest_sink.
  nnscustom_framecounter = shared_library('nnscustom_framecounter',
    'nnstreamer_sink/nnscustom_framecounter.c',
    c_args: nnstreamer_base_args,
    dependencies: [nnstreamer_deps],
    objects: [tensor_commonOBJ],
    include_directories: nnstreamer_inc)

  # Run unittest_common
  unittest_common = executable('unittest_common',
    'common/unittest_common.cpp',
    cpp_args: nnstreamer_base_args,
    dependencies: [nnstreamer_deps, gtest_dep],
    objects: [tensor_commonOBJ],
    include_directories: nnstreamer_inc)

  test('unittest_common', unittest_common)

  # Run unittest_sink
  unittest_sink = executable('unittest_sink',
    'nnstreamer_sink/unittest_sink.cpp',
    cpp_args: nnstreamer_base_args,
    dependencies: [nnstreamer_deps, gtest_dep, gst_app_dep],
    objects: [tensor_commonOBJ],
    include_directories: nnstreamer_inc)

  test('unittest_sink', unittest_sink, args: ['--gst-plugin-path=../'])

  # Run unittest_plugins
  unittest_plugins = executable('unittest_plugins',
    'nnstreamer_plugins/unittest_plugins.cpp',
    cpp_args: nnstreamer_base_args,
    dependencies: [nnstreamer_deps, gtest_dep, gst_check_dep],
    objects: [tensor_commonOBJ, tensor_transformOBJ],
    include_directories: nnstreamer_inc)

  test('unittest_plugins', unittest_plugins, args: ['--gst-plugin-path=../'])
endif
