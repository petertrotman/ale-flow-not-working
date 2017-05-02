# A demonstration project to show that Vim ALE does not correctly use the JavaScript Flow linter.

## Steps to reproduce:

- Clone the repository
- `npm install`
- Open `index.js` - no errors
- (optional) Remove the `/* eslint-disable no-console */` comment to show that ALE is correctly using ESLint
- Note that there should be an error from Flow when we call `square('hello')`
- `npm run flow` -> Error is correctly identified, but not displayed in Vim with ALE

## ALEInfo

```
:ALEInfo

Current Filetype: javascript.jsx
Available Linters: ['eslint', 'flow', 'jscs', 'jshint', 'standard', 'xo']
Enabled Linters: ['eslint', 'flow', 'jscs', 'jshint', 'standard', 'xo']
Linter Variables:
let g:ale_javascript_eslint_executable = 'eslint'
let g:ale_javascript_eslint_options = ''
let g:ale_javascript_eslint_use_global = 0
let g:ale_javascript_flow_executable = 'flow'
let g:ale_javascript_flow_use_global = 0
let g:ale_javascript_jshint_executable = 'jshint'
let g:ale_javascript_jshint_use_global = 0
let g:ale_javascript_standard_executable = 'standard'
let g:ale_javascript_standard_options = ''
let g:ale_javascript_standard_use_global = 0
let g:ale_javascript_xo_executable = 'xo'
let g:ale_javascript_xo_options = ''
let g:ale_javascript_xo_use_global = 0
Global Variables:
let g:ale_echo_cursor = 1
let g:ale_echo_msg_error_str = 'Error'
let g:ale_echo_msg_format = '%s'
let g:ale_echo_msg_warning_str = 'Warning'
let g:ale_enabled = 1
let g:ale_keep_list_window_open = 0
let g:ale_lint_delay = 200
let g:ale_lint_on_enter = 1
let g:ale_lint_on_save = 1
let g:ale_lint_on_text_changed = 'always'
let g:ale_linter_aliases = {}
let g:ale_linters = {}
let g:ale_open_list = 0
let g:ale_set_highlights = 1
let g:ale_set_loclist = 1
let g:ale_set_quickfix = 0
let g:ale_set_signs = 1
let g:ale_sign_column_always = 0
let g:ale_sign_error = '>>'
let g:ale_sign_offset = 1000000
let g:ale_sign_warning = '--'
let g:ale_statusline_format = ['%d error(s)', '%d warning(s)', 'OK']
let g:ale_warn_about_trailing_whitespace = 1
Command History:
(finished - exit code 0) ['/usr/bin/zsh', '-c', '/home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/node_modules/eslint/bin/eslint.js  -f unix --stdin --stdin-filename /home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/index.js < /tmp/vWhD7mJ/0/index.js']

(finished - exit code 0) ['/usr/bin/zsh', '-c', '/home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/node_modules/.bin/flow check-contents --respect-pragma --json --from ale /home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/index.js < /tmp/vWhD7mJ/1/index
.js']
(finished - exit code 0) ['/usr/bin/zsh', '-c', '/home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/node_modules/eslint/bin/eslint.js  -f unix --stdin --stdin-filename /home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/index.js < /tmp/vWhD7mJ/2/index.js']

<<<NO OUTPUT RETURNED>>>
(finished - exit code 0) ['/usr/bin/zsh', '-c', '/home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/node_modules/.bin/flow check-contents --respect-pragma --json --from ale /home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/index.js < /tmp/vWhD7mJ/3/index
.js']
<<<NO OUTPUT RETURNED>>>
```

## Manually running commands

1. ESLint - With `/* eslint-disable no-console */`

```
$ /home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/node_modules/eslint/bin/eslint.js  -f unix --stdin --stdin-filename /home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/index.js < /home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/index.js
```

(Nothing is output)

```
$ echo $?
0
```

2. ESLint - Without `/* eslint-disable no-console */`

```
$ /home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/node_modules/eslint/bin/eslint.js  -f unix --stdin --stdin-filename /home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/index.js < /home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/index.js
/home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/index.js:7:1: Unexpected console statement. [Error/no-console]
/home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/index.js:8:1: Unexpected console statement. [Error/no-console]

2 problems
```

```
$ echo $?
1
```

3. Flow

```
$ /home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/node_modules/.bin/flow check-contents --respect-pragma --json --from ale /home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/index.js < /home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/index.js
{"flowVersion":"0.45.0","errors":[{"kind":"infer","level":"error","message":[{"context":"console.log(square('hello'));","descr":"string","type":"Blame","loc":{"source":"/home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/index.js","type":"SourceFile","start":{"line":9,"column":20,"offset":135},"end":{"line":9,"column":26,"offset":142}},"path":"/home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/index.js","line":9,"endline":9,"start":20,"end":26},{"context":null,"descr":"This type is incompatible with the expected param type of","type":"Comment","path":"","line":0,"endline":0,"start":1,"end":0},{"context":"function square(n: number) {","descr":"number","type":"Blame","loc":{"source":"/home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/index.js","type":"SourceFile","start":{"line":4,"column":20,"offset":61},"end":{"line":4,"column":25,"offset":67}},"path":"/home/peter/dev/src/github.com/petertrotman/ale-flow-not-working/index.js","line":4,"endline":4,"start":20,"end":25}]}],"passed":false}% 
```

So error message is there, but ALE isn't making use of it. My guess is because...

```
$ echo $?
0
```

## Conclusion

Flow returns a 0 status when an error is identified. This makes sense to me because Flow runs fine - so no errors, but in running fine it identified an error.

However, when running `:ALEInfo` after `:ALELint` with `:let g:ale_history_log_output = 1` (as shown above), it does state that there is `<<<NO OUTPUT RETURNED>>>` which confuses me, because when running the command manually it does produce output. I wonder then if there is some configuration that I haven't done properly?

So my guess is that ALE is ignoring the Flow output because it returns 0. I had a quick look and I can't find a Flow CLI option to return an error if errors are found.

Thoughts? I wonder if this worked in the past but Flow has changed its output to something that no longer works with ALE. I'm very keen for this to get this working as soon as possible. Thoughts?

