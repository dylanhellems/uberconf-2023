# Super Charge Your Dev Environment

> "Use tools that allow you to be flawed"

Speaker: Ken Sipe

- [Super Charge Your Dev Environment](#super-charge-your-dev-environment)
  - [Quick Tips](#quick-tips)
  - [zshell](#zshell)
  - [ngrok](#ngrok)

## Quick Tips

- `esc+.` to quick fill last touched file
- `cd - + tab` to show recent dirs
- `take <dir>` make and move to dir or move to existing dir
  - works with path as well
- `cmd+k` to clear and remove history
- `ctrl+l` to clear and keep history
- `tree` to show directory structure
  - `exa --icons -T -L <depth>` prettier alternative
- `trash` sends files and folders to trash can
- `tldr <command>` more concise man

## zshell

- Oh My
  - [omz](https://ohmyz.sh/)
  - an open source community-driven framework for managing configuration
  - can use plugins to customize
    - autojump
      - `j <partial path>` to jump to matching recent directory
      - `j -i <value>` to increase the weight of a directory, more likely to be jumped to in future
      - `j -s` to show weights
    - brew
      - `bubu` to upgrade outdated
    - encode64
    - git
      - `groh` undo everything and make it consistent with origin branch
      - `gcm` got to default branch
      - `gpsup` git push to upstream
    - git-extras
    - helm
    - sudo
      - `esc+esc` to add or remove sudo
    - zsh-z
    - zsh-syntax-highlighting
      - Shows if current typed command is valid
    - zsh-autosuggestions
      - arrow over to complete
  - use `powerloevel10k` theme
  - use Nerd Fonts
    - MesloLGX NF
    - Can add to ide terminals as well

## ngrok

- Secure introspectable tunnels to localhost
- `ngrok` is a simplified API-first ingress-as-a-service that adds connectivity, security, and observability
- [Running locally debugging in an editor](https://kudo.dev/blog/blog-2020-07-10-webhook-development.html#running-locally-debugging-in-an-editor)
