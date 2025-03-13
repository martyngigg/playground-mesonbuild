python_sources = [
  '__init__.py',
]

py.install_sources(
  python_sources,
  pure: false,
  subdir: 'f2py_examples'
)

gen_fwrappers = custom_target('gen-fwrappers',
                        input: 'fib1.f',
                        output: ['fibmodule.c'],
                        command: [py, '-m', 'numpy.f2py', '@INPUT@', '-m', 'fib', '--build-dir', '@OUTDIR@'])

py.extension_module('fib',
  [
    'fib1.f',
    gen_fwrappers[0],
  ],
  incdir_f2py / 'fortranobject.c',
  include_directories: inc_np,
  dependencies : [py_dep],
  install : true,
  subdir: 'f2py_examples'
)
