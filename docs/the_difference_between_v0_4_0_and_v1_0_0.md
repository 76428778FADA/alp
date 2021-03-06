# The difference between v0.4.0 and v1.0.0

- Supports log formats other than LTSV
    - JSON
    - regexp
- Sub-commands are added for each format to support multiple log formats.
    - The `--xxx-label` option of LTSV is changed to `alp ltsv`
- Reduction and integration of options.
    - Sort option was integrated into `--sort=SORT`
- The `--tsv` option was changed to `--format=(table|tsv)`
- Supports filtering of profile results by the `--filters` option
    - Removed `--includes`, `--excludes`, `--start-time`, `--end-time`, `--start-time-duration`, `--end-time-duration` as they are no longer needed
- Rename from `--aggregates` to `-m, --matching-groups`
- Supports change the output of the profile results by using the `-o, --output`
- The `--pos` option allows you to record the number of bytes parsed, and to parse subsequent bytes in the next cycle
    - You don't have to truncate the log file every time you run benchmarks
- Change the default `--sort` option from `max` to `count`

## References

### v0.4.0 options

```console
$ 
$ alp --help
usage: alp [<flags>]

Access Log Profiler for LTSV (read from file or stdin).

Flags:
      --help                     Show context-sensitive help (also try --help-long and --help-man).
  -c, --config=CONFIG            config file
  -f, --file=FILE                access log file
  -d, --dump=DUMP                dump profile data
  -l, --load=LOAD                load profile data
      --max                      sort by max response time
      --min                      sort by min response time
      --avg                      sort by avg response time
      --sum                      sort by sum response time
      --cnt                      sort by count
      --uri                      sort by uri
      --method                   sort by method
      --max-body                 sort by max body size
      --min-body                 sort by min body size
      --avg-body                 sort by avg body size
      --sum-body                 sort by sum body size
      --p1                       sort by 1 percentail response time
      --p50                      sort by 50 percentail response time
      --p99                      sort by 99 percentail response time
      --stddev                   sort by standard deviation response time
  -r, --reverse                  reverse the result of comparisons
  -q, --query-string             include query string
      --tsv                      tsv format (default: table)
      --apptime-label="apptime"  apptime label
      --reqtime-label="reqtime"  reqtime label
      --status-label="status"    status label
      --size-label="size"        size label
      --method-label="method"    method label
      --uri-label="uri"          uri label
      --time-label="time"        time label
      --limit=5000               set an upper limit of the target uri
      --location=LOCATION        location name
      --includes=PATTERN,...     don't exclude uri matching PATTERN (comma separated)
      --excludes=PATTERN,...     exclude uri matching PATTERN (comma separated)
      --include-statuses=PATTERN,...
                                 don't exclude status code matching PATTERN (comma separated)
      --exclude-statuses=PATTERN,...
                                 exclude uri status code PATTERN (comma separated)
      --noheaders                print no header line at all (only --tsv)
      --aggregates=PATTERN,...   aggregate uri matching PATTERN (comma separated)
      --start-time=TIME          since the start time
      --end-time=TIME            end time earlier
      --start-time-duration=TIME_DURATION
                                 since the start time (now - time.Duration)
      --end-time-duration=TIME_DURATION
                                 end time earlier (now - time.Duration)
      --version                  Show application version.
```

### v1.0.0 options and Sub-commands

```console
$ alp --help
usage: alp [<flags>] <command> [<args> ...]

alp is the access log profiler for LTSV, JSON, and others.

Flags:
      --help               Show context-sensitive help (also try --help-long and --help-man).
  -c, --config=CONFIG      The configuration file
      --file=FILE          The access log file
  -d, --dump=DUMP          Dump profiled data as YAML
  -l, --load=LOAD          Load the profiled YAML data
      --sort=max           Output the results in sorted order
  -r, --reverse            Sort results in reverse order
  -q, --query-string       Include the URI query string.
      --format=table       The output format (table or tsv)
      --noheaders          Output no header line at all (only --format=tsv)
      --show-footers       Output footer line at all (only --format=table)
      --limit=5000         The maximum number of results to display.
      --location="Local"   Location name for the timezone
  -o, --output="all"       Specifies the results to display, separated by commas
  -m, --matching-groups=PATTERN,...
                           Specifies URI matching groups separated by commas
  -f, --filters=FILTERS    Only the logs are profiled that match the conditions
      --pos=POSITION_FILE  The position file
      --nosave-pos         Do not save position file
      --version            Show application version.

Commands:
  help [<command>...]
    Show help.

  ltsv [<flags>]
    Profile the logs for LTSV

  json [<flags>]
    Profile the logs for JSON

  regexp [<flags>]
    Profile the logs that match a regular expression
```

```console
$ alp ltsv --help
usage: alp ltsv [<flags>]

Profile the logs for LTSV

Flags:
...
      --uri-label=uri          Change the uri label
      --method-label=method    Change the method label
      --time-label=time        Change the time label
      --apptime-label=apptime  Change the apptime label
      --reqtime-label=reqtime  Change the reqtime label
      --size-label=size        Change the size label
      --status-label=status    Change the status label
```

```console
$ alp json --help
usage: alp json [<flags>]

Profile the logs for JSON

Flags:
...
      --uri-key=uri        Change the uri key
      --method-key=method  Change the method key
      --time-key=time      Change the time key
      --restime-key=response_time
                           Change the response_time key
      --reqtime-key=request_time
                           Change the request_time key
      --body-bytes-key=body_bytes
                           Change the body_bytes key
      --status-key=status  Change the status key
```

```console
$ alp regexp --help
usage: alp regexp [<flags>]

Profile the logs that match a regular expression

Flags:
...
      --pattern=PATTERN       Regular expressions pattern matching the log
      --uri-subexp=uri        Change the uri sub expression
      --method-subexp=method  Change the method sub expression
      --time-subexp=time      Change the time sub expression
      --restime-subexp=response_time
                              Change the response_time sub expression
      --reqtime-subexp=request_time
                              Change the request_time sub expression
      --body-bytes-subexp=body_bytes
                              Change the body_bytes sub expression
      --status-subexp=status  Change the status sub expression
```
