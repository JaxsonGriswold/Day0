=========================suspicious ports================================
  patterns, consecutive numbers, etc
linux = netstat -ant or -ltup (use sudo to get PIDs)
order of operations
    - find sus port
    - look at process listing/pid/services to find what's running it
          - might be some sort of script or configuration with it you want to look at
    - look for persistance

windows = netstat /ano
tasklist
look for processes = get-process -id <PID>
windows artifacts 
    decode userassist (rot13) and/or check others
check for persistence 
don't be afraid to use sysinternal tools like procmon, autoruns, etc (steps to download/use on fg)
        within autoruns click on options and uncheck hide windows entries
=====================================================
