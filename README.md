# hyprland

Dotfiles for my workstation, nothing in here is clever — it just happens to suit the way I work.

- **Box**: HP Omen 16 (u0032np)
- **Distro**: EndeavourOS
- **Compositor**: hyprland
- **Terminal**: alacritty
- **Interactive shell**: zsh
- **Text editor**: helix (config on a keymap of its own)
- **Session tool**: tmux
- **Top bar**: wlroots statusbar with
  - clock + calendar popup
  - speaker level
  - battery percentage
  - occupied workspaces as dots
- **Run dialog**: fuzzel, plain fuzzy search
- Session starts from a plain TTY
- Lazy on CPU, no compositor daemon dance
- Enough for a full day of work

(Steal whatever seems useful, though expect the defaults to change on a whim.)

> [!NOTE]
> The bar is a single binary reading one config, so nothing here links against a desktop environment.

> [!TIP]
> Themes live next to the configs — swap one file and reload, no session restart needed.

Layers start at boot and stack in this order:

1. `systemd` → grabs the TTY, drops the greetd unit
2. `greetd` → hands the session to the compositor
3. `hyprland` → publishes the socket, spawns the bar
4. `alacritty` → asks the session bus for a window
5. `tmux` → attaches, restores the old layout

The bar is driven by a small listener, not by polling:

    $ barctl status
    clock      tick 1000ms   sync: drift 2ms
    speaker    pactl subscribe
    battery    sysfs reader   level 87%   charging off
    workspace  compositor socket  dots: 1 3
    $

<details>
<summary>Why the shell is zsh and not fish</summary>

Completion for the handful of CLIs I use daily was already written for the POSIX-like dialect. Rewriting it was not worth the afternoon.

</details>

Order of the keys I reach for:

| chord | lands on |
|---|---|
| `Super` + `Return` | new terminal |
| `Super` + `Q` | close the focused window |
| `Super` + `Tab` | scratchpad toggle |
| `Alt` + `1`..`4` | workspace jump |