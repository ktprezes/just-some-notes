# Some pacman notes

_The best known **pacman** is legacy tv / console game,_<br>
_but this memo is rather about [default Arch Linux Package Manager](https://wiki.archlinux.org/index.php/pacman)_

---

## Sections

- [Update packages from specific repository](#specificrepoupdate)
- ['No space left on device' message](#nospaceleftmsg)
- [Some other pacman related links](#otherlinks)
- [Return to...](#returnto)

---

## <a name="specificrepoupdate"></a>When you want to update packages installed in your system,<br/>&emsp;&ensp;but only from specific repository (e.g. core).</a>

```bash
    pacman -S --needed $(comm -12 <(pacman -Qq | sort) <(pacman -Slq core | sort))
```

### A bit of explanation - Newbie corner:

- `pacman -Qq` lists in short form (only names, without version info)<br>all packages installed in your system - one package in a row
- `pacman -Slq core` lists in short form all packages in [core] repository - one package in a row
- Two `| sort` commands sort theses lists
- `comm -12 <(..) <(..)` puts both sorted lists to comm's standard input; <br>the comm command compares them and returns third one consisting only of their common rows
- `$(..)` transforms this list of common rows <br>from 'new-line-separated' to 'space-separated' form
- Finally `pacman -S --needed $(..)` takes this space-separated list of packages <br>from [core] repository installed in your system and updates them :)

---

## <a name="nospaceleftmsg">When you want to install or upgrade some package(s)<br/>&emsp;&ensp;and receive the _'there is no space left on device'_ message.</a>

Most probably you receive this message because of lack of space in _/tmp_ folder;<br>
by default it's capacity equals half of your RAM.<br>
IMHO the easiest way to deal with it is to use _yaourt_ instead of _pacman_.<br>
With _yaourt_ you can set different _/tmp_ folder.

- first of all you have to install it, e.g.: `pacman -S yaourt`
- when you want to install / upgrade some package(s), use:<br/> `yaourt -S package-name --tmp /your-temp-folder`
- of course you should use _/your-temp-folder_ located on disk / device<br>
  with enough amount of free space left :)

---

...

---

## <a name="otherlinks">Links to many more pacman notes / tips.</a>

- https://wiki.archlinux.org/index.php/Pacman
- https://wiki.archlinux.org/index.php/Pacman/Tips_and_tricks
- https://wiki.archlinux.org/index.php/Pacman/Rosetta
- https://www.lifewire.com/using-the-pacman-package-manager-4018823
- https://taleofcoder.wordpress.com/2019/01/13/a-guide-to-use-pacman-package-manager-tips-tricks/
- https://www.ostechnix.com/use-archlinuxs-pacman-package-manager-unix-like-oss/
- https://wiki.manjaro.org/index.php?title=Pacman_Tips
- https://devhints.io/pacman

---

## <a name="returnto">Return to:</a>

- [Repository home page](../README.md)
- [My GitHub account home page](https://github.com/ktprezes)
