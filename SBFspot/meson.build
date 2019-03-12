db_opt = get_option('db_opt')

# sources, sqlite-only for now
no_sql_sources = files(['boost_ext.cpp', 'misc.cpp', 'sunrise_sunset.cpp', 'SBFNet.cpp', 'CSVexport.cpp', 
                       'Ethernet.cpp', 'EventData.cpp', 'ArchData.cpp', 'SBFspot.cpp', 'TagDefs.cpp', 'Bluetooth.cpp'])
sqlite_sources = no_sql_sources + files(['db_SQLite.cpp', 'db_SQLite_Export.cpp'])
mariadb_sources = no_sql_sources + files(['db_MySQL.cpp', 'db_MySQL_Export.cpp'])

# dependencies
thread_dep = dependency('threads')
bluetooth_dep = dependency('bluez')
boost_dep = dependency('boost', modules: ['date_time', 'system', 'filesystem', 'regex'])
sqlite_dep = dependency('sqlite3')
mariadb_dep = dependency('libmariadb')

# and finally the executable
if db_opt == 'sqlite'
  executable('sbfspot', sqlite_sources,
             dependencies : [thread_dep, bluetooth_dep, boost_dep, sqlite_dep],
	     cpp_args : '-DUSE_SQLITE')
endif

if db_opt == 'mariadb'
  executable('sbfspot', mariadb_sources,
             dependencies : [thread_dep, bluetooth_dep, boost_dep, mariadb_dep],
	     cpp_args : '-DUSE_MYSQL')
endif

