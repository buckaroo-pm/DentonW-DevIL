load('//:subdir_glob.bzl', 'subdir_glob')
load('//:buckaroo_macros.bzl', 'buckaroo_deps')

genrule(
  name = 'config',
  out = 'config.h',
  cmd = 'touch $OUT'
)
  
cxx_library(
  name = 'devil-headers',
  header_namespace = '',
  exported_headers = subdir_glob([ 
    ('DevIL/include', '**/*.h'),
  ]),
  visibility = ['PUBLIC']
)

cxx_library(
  name = 'devil-il',
  header_namespace = '',
  exported_headers = dict(subdir_glob([
    ('DevIL/src-IL/include', '**/*.h')
  ]).items() + [('IL/config.h', ':config')]),
  deps = [':devil-headers'] + buckaroo_deps(),
  srcs = glob([
    'DevIL/src-IL/src/*.cpp'
  ]),
  visibility = ['PUBLIC']
)

cxx_library(
  name = 'devil-ilu',
  header_namespace = '',
  exported_headers = subdir_glob([
    ('DevIL/src-ILU/include', '**/*.h')
  ]),
  deps = [':devil-headers'],
  srcs = glob([
    'DevIL/src-ILU/src/*.cpp'
  ]),
  visibility = ['PUBLIC']
)

cxx_library(
  name = 'devil-ilut',
  header_namespace = '',
  exported_headers = subdir_glob([
    ('DevIL/src-ILUT/include', '**/*.h')
  ]),
  deps = [':devil-headers'],
  srcs = glob([
    'DevIL/src-ILUT/src/*.cpp'
  ]),
  visibility = ['PUBLIC']
)

cxx_binary(
  name = 'ilur',
  srcs = ['DevIL/src-ILU/ilur/ilur.c'],
  deps = [':devil-il', ':devil-ilu', ':devil-ilut'],
  visibility = ['PUBLIC'] 
)

