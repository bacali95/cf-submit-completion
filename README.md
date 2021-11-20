# cf-submit-completion

## Installation

### Using [Antigen](https://github.com/zsh-users/antigen)

Bundle `cf-submit-completion` in your `.zshrc`

```shell
antigen bundle bacali95/cf-submit-completion
```

### Using [zplug](https://github.com/b4b4r07/zplug)

Load `zsh-better-npm-completion` as a plugin in your `.zshrc`

```shell
zplug "bacali95/cf-submit-completion", nice:10

```

### Using [zgen](https://github.com/tarjoilija/zgen)

Include the load command in your `.zshrc`

```shell
zgen load bacali95/cf-submit-completion
```

### As an [Oh My ZSH!](https://github.com/robbyrussell/oh-my-zsh) custom plugin

Clone `cf-submit-completion` into your custom plugins repo

```shell
git clone https://github.com/bacali95/cf-submit-completion ~/.oh-my-zsh/custom/plugins/cf-submit-completion
```

Then load as a plugin in your `.zshrc`

```shell
plugins+=(cf-submit-completion)
```

### Manually

Clone this repository somewhere (`~/.cf-submit-completion` for example)

```shell
git clone https://github.com/bacali95/cf-submit-completion.git ~/.cf-submit-completion
```

Then source it in your `.zshrc`

```shell
source ~/.cf-submit-completion/cf-submit-completion.plugin.zsh
```

## License

MIT © Nasreddine Bac Ali
