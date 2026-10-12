project('mainserver', 'cpp',
  version : '0.1',
  default_options : ['cpp_std=c++11', 'warning_level=1'])

thread_dep = dependency('threads')

sources = files(
  'Chrono.cpp',
  'Console.cpp',
  'Manager.cpp',
  'Payload.cpp',
  'Profiler.cpp',
  'RequestInfo.cpp',
  'StreamClient.cpp',
  'StreamPayload.cpp',
  'StreamServer.cpp',
  'StreamVector.cpp',
  'TCPListener.cpp',
  'TCPRequestInfo.cpp',
  'TCPResponse.cpp',
  'TCPSegment.cpp',
  'ThreadPool.cpp',
  'UDPDatagram.cpp',
  'UDPListener.cpp',
  'UDPRequestInfo.cpp',
  'UDPResponse.cpp',
  'UDPSender.cpp',
  'mainserver.cpp',
  'utils.cpp',
)

executable('mainserver', sources,
  dependencies : thread_dep,
  cpp_args : get_option('buildtype').startswith('debug') ? ['-DDEBUG', '-DVERBOSENESS=2'] : [])
