project('f2py_examples', 'c',
  version : '0.1',
  license: 'BSD-3',
  meson_version: '>=0.64.0',
  default_options : ['warning_level=2'],
)

add_languages('fortran')

py_mod = import('python')
py = py_mod.find_installation(pure: false)
py_dep = py.dependency()

incdir_numpy = run_command(py,
  ['-c', 'import os; os.chdir(".."); import numpy; print(numpy.get_include())'],
  check : true
).stdout().strip()

incdir_f2py = run_command(py,
    ['-c', 'import os; os.chdir(".."); import numpy.f2py; print(numpy.f2py.get_include())'],
    check : true
).stdout().strip()

inc_np = include_directories(incdir_numpy, incdir_f2py)


gen_fwrappers = custom_target('gen-fwrappers',
                        input: 'fib1.f',
                        output: ['fibmodule.c', 'fib-f2pywrappers.f'],
                        command: [py, '-m', 'numpy.f2py', '@INPUT@', '-m', 'fib'])

py.extension_module('fib',
  [
    'fib1.f',
    gen_fwrappers[0],
  ],
  incdir_f2py / 'fortranobject.c',
  include_directories: inc_np,
  dependencies : [py_dep],
  install : true
)
