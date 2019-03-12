# switches
db_opt = get_option('db_opt')

# sources
common_sources_path = ('../SBFspotUploadCommon')
sbfspot_sources_path = ('../SBFspot')
main_sources = files('main.cpp', common_sources_path + '/Configuration.cpp', common_sources_path + '/CommonServiceCode.cpp', 
	             common_sources_path + '/PVOutput.cpp', common_sources_path + '/PVOutput_x.cpp')
sqlite_sources = main_sources + files(sbfspot_sources_path + '/db_SQLite.cpp')
mariadb_sources = main_sources + files(sbfspot_sources_path + '/db_MySQL.cpp')

# include dir
inc = include_directories('../SBFspot')

# dependencies
thread_dep = dependency('threads')
curl_dep = dependency('libcurl')
sqlite_dep = dependency('sqlite3')
mariadb_dep = dependency('libmariadb')

# take care of the version
pre_args = ('-DPACKAGE_VERSION="@0@"'.format(meson.project_version()))

# and finally the executable
if db_opt == 'sqlite'
  executable('sbfspotuploadd', sqlite_sources,
	     dependencies : [thread_dep, curl_dep, sqlite_dep],
	     include_directories : inc,
	     cpp_args : '-DUSE_SQLITE')
endif

if db_opt == 'mariadb'
  executable('sbfspotuploadd', mariadb_sources,
	     dependencies : [thread_dep, curl_dep, mariadb_dep],
	     include_directories : inc,
	     cpp_args : '-DUSE_MYSQL')
endif
