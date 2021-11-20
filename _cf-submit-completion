#compdef cf

_commands=(
  'login:Save your Codeforces login info'
  'info:Print the current config'
  'con:Change default contest ID in config'
  'contests:Print the list of contests in decreasing order'
  'gym:Change default gym ID in config'
  'gyms:Print the list of gyms in decreasing order'
  'gcon:Change default group ID and group contest ID in config'
  'groups:Print the list of your groups'
  'gcontests:Print the list of group contests in decreasing order'
  'problems:Print the list of problems of the preconfigured contest'
  'standings:Print the standings of the preconfigured contest'
  'open:Open a choosen problem in browser'
  'parse:Parse input/output files of a choosen problem and save them under $PWD/files'
  'test:Run your main file with the parsed files with `cf parse` and print the result'
  'submit:Submit your main file to codeforces'
  'watch:Print a live status of the last submission'
  'peek:Print a latest status of the last submission'
  'time:Print the time of the preconfigured contest'
  'hack:Start hacking process for a specific problem in Educational/Div.3 contests'
  'version:Print the version of cf script'
)

_subcommands=(
  'standings:Print the standing of the hackers'
  $(ls)
)

__get_index() {
  for ((index = 1; index <= ${#ARRAY[@]}; index++)); do
    if [[ "${ARRAY[$index]}" == "$VALUE" ]]; then
      echo $index
      return
    fi
  done
  echo -1
}

__cf_contest_ids() {
  [[ $PREFIX = -* ]] && return 1
  integer ret=1
  ids=$(cf contests --pretty-off)
  _alternative "args:contest_id:($ids)" && ret=0

  return ret
}

__cf_gym_ids() {
  [[ $PREFIX = -* ]] && return 1
  integer ret=1
  ids=$(cf gyms --pretty-off)
  _alternative "args:gym_id:($ids)" && ret=0

  return ret
}

__cf_group_ids() {
  [[ $PREFIX = -* ]] && return 1
  integer ret=1
  ids=$(cf groups --pretty-off)
  _alternative "args:group_id:($ids)" && ret=0

  return ret
}

__cf_group_contest_ids() {
  [[ $PREFIX = -* ]] && return 1
  integer ret=1
  ARRAY=($words)
  VALUE='--group'
  index=$(__get_index)
  if [[ ! $index -eq -1 ]]; then
    ids=$(cf gcontests --group ${words[$index + 1]} --pretty-off)
    _alternative "args:group_id:($ids)" && ret=0
  fi

  return ret
}

__cf_problems() {
  [[ $PREFIX = -* ]] && return 1
  integer ret=1
  ids=$(cf problems --pretty-off)
  _alternative "args:problem:($ids)" && ret=0

  return ret
}

__cf_langs() {
  [[ $PREFIX = -* ]] && return 1
  integer ret=1
  langs=(cpp c d py rb kt java scala rs php)
  _alternative "args:problem:($langs)" && ret=0

  return ret
}

__cf_standings_contest_ids() {
  [[ $PREFIX = -* ]] && return 1
  integer ret=1
  ARRAY=($words)
  VALUE='--group'
  index=$(__get_index)
  if [[ ! $index -eq -1 ]]; then
    ids=$(cf gcontests --group ${words[$index + 1]} --pretty-off)
    _alternative "args:group_id:($ids)" && ret=0
  else
    cids=$(cf contests --pretty-off)
    gids=$(cf gyms --pretty-off)
    _alternative "args:group_id:($cids $gids)" && ret=0
  fi

  return ret
}

_cf_commands() {
  _describe 'command' _commands
}

_cf_subcommands() {
  integer ret=1
  case $words[1] in
  login)
    _arguments \
      '--handle[Your Codeforces handle]' && ret=0
    ;;
  con)
    _arguments \
      '--id[Codeforces contest id]:contest_id:__cf_contest_ids' && ret=0
    ;;
  gym)
    _arguments \
      '--id[Codeforces gym id]:gym_id:__cf_gym_ids' && ret=0
    ;;
  gcon)
    _arguments \
      '--group[Codeforces group id]:group_id:__cf_group_ids' \
      '(-c --contest)'{-c,--contest}'[Codeforces group contest id]:contest_id:__cf_group_contest_ids' && ret=0
    ;;
  contests | gyms | groups | problems)
    _arguments '--pretty-off[Turn off pretty printing]' && ret=0
    ;;
  gcontests)
    _arguments \
      '--group[Codeforces group id]:group_id:__cf_group_ids' \
      '--pretty-off[Turn off pretty printing]' && ret=0
    ;;
  standings)
    _arguments \
      '(-a --all)'{-a,--all}'[Print full standings]' \
      '(-t --top)'{-t,--top}'[Print n top players]:top:($(seq 1 1 10))' \
      '(-s --sort)'{-s,--sort}'[Sort standings]:sort:(solves index id)' \
      '(-c --contest)'{-c,--contest}'[Codeforces contest id]:contest_id:__cf_standings_contest_ids' \
      '--group[Codeforces group id]:group_id:__cf_group_ids' \
      '--pretty-off[Turn off pretty printing]' \
      '--verbose' && ret=0
    ;;
  open | parse)
    _arguments \
      '(-p --prob)'{-p,--prob}'[Codeforces problem letter]:problem:__cf_problems' && ret=0
    ;;
  test)
    _arguments \
      '1:files:($(ls))' && ret=0
    ;;
  submit)
    _arguments \
      '(-l --lang)'{-l,--lang}'[Main file language]:lang:__cf_langs' \
      '(-p --prob)'{-p,--prob}'[Codeforces problem letter]:problem:__cf_problems' \
      '(-w --watch)'{-w,--watch}'[Print live submission status]' \
      '1:files:($(ls))' && ret=0
    ;;
  hack)
    if [[ "$words[2]" == "standings" ]]; then
      _arguments \
        '(-a --all)'{-a,--all}'[Print full standings]' \
        '(-t --top)'{-t,--top}'[Print n top players]:top:($(seq 1 1 10))' \
        '(-c --contest)'{-c,--contest}'[Codeforces contest id]:contest_id:__cf_standings_contest_ids' \
        '*: :()' && ret=0
    elif [[ "${#words[@]}" -gt 2 ]]; then
      _arguments \
        '(-n --number)'{-n,--number}'[Number of tests]:tests:($(seq 1 1 20))' \
        '(-p --prob)'{-p,--prob}'[Codeforces problem letter]:problem:__cf_problems' \
        '(-r --reverse)'{-r,--reverse}'[Hack the submissions in reverse order]' \
        '--time-limit[Timelimit to use]' \
        '1:generator-source:($(ls))' \
        '2:tle-generator-source:($(ls))' \
        '3:checker-source:($(ls))' \
        '4:source-source:($(ls))' && ret=0
    else
      _describe 'command' _subcommands
    fi
    ;;
  *)
    _message 'Unknown sub command' && ret=1
    ;;
  esac

  return ret
}

_cf() {
  local context state state_descr line
  integer ret=1

  _arguments \
    '(-h --help)'{-h,--help}'[output usage information]' \
    '1: :->command' \
    '(-)*:: :->option-or-argument' && ret=0

  case $state in
  command)
    _cf_commands && ret=0
    ;;
  option-or-argument)
    _cf_subcommands && ret=0
    ;;
  esac

  return ret
}

_cf "$@"

# Local Variables:
# mode: Shell-Script
# sh-indentation: 2
# indent-tabs-mode: nil
# sh-basic-offset: 2
# End:
# vim: ft=zsh sw=2 ts=2 et
