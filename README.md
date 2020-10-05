
# Table of Contents

1.  [What is this?](#org8a95856)
2.  [Installation](#org9307576)
    1.  [AUR](#org494b16f)
    2.  [crates.io (rusts package manager)](#org5820fa8)
    3.  [From the release page](#orga6989f6)
    4.  [compile manually](#org3b6c0cf)
3.  [Usage:](#orga9ef129)
4.  [Security](#orgbc244a8)

yas - a (kind of) sudo replacement

(entire readme is still work in progress)


<a id="org8a95856"></a>

# What is this?

yas, or &rsquo;yet another sudo&rsquo;, is kind of a sudo replacement, written in rust and without really any configuration options or not needed features.
It is intended for single user systems only, as it works out of the box, with no configuration needed, but you also can&rsquo;t restrict a user from running stuff as root.
yas also can&rsquo;t run commands as any other user, but root.
In case you really do have a user, that shouldn&rsquo;t be allowed to run stuff as root, this isn&rsquo;t for you.


<a id="org9307576"></a>

# Installation


<a id="org494b16f"></a>

## AUR

There is a AUR package for the git version of yas, you can install it with a AUR helper, or just git clone it manually:
Replace yas-git with yas-tui-git for a tui version.

    git clone ssh://aur@aur.archlinux.org/yas-git.git
    cd yas-git
    makepkg -is

or (for yay):

    yay -S yas-git


<a id="org5820fa8"></a>

## crates.io (rusts package manager)

Get it from crates.io with rusts cargo, by running:

    cargo install yas

NOTE: The suid bit will not be set, you will manually have to set it for yas to work:

    su -c "chown root ~/.cargo/bin/yas && chmod u+s ~/.cargo/bin/yas"


<a id="orga6989f6"></a>

## From the release page

If you get a libc error when running, you should compile it from source, this will happen espcially often with distros that are debian based.
Or you can get the release from the release page with \`-musl\`, note that there isn&rsquo;t a tui build for that, because ncurses fails to compile. You will have to compile it manually then.

1.  Download a binary
2.  Change the owner to root

    chmod root yas

1.  Set the suid bit

    chmod u+s yas

1.  Put it somewhere in your path, such as /usr/bin


<a id="org3b6c0cf"></a>

## compile manually

1.  Install rust (<https://www.rust-lang.org/>)
2.  Clone the source
3.  build it in release mode, either with tui or not

\`\`\`
git clone <https://github.com/alx365/yas.git>

cargo build &#x2013;release # if with tui, add the \`&#x2013;features &ldquo;tui&rdquo;\` flag

strip target/release/yas
\`\`\`

1.  Change the owner to root

    chmod root yas

1.  Set the suid bit

    chmod u+s yas


<a id="orga9ef129"></a>

# Usage:

    yas - execute commands as the root user
    
    usage: yas [-h/--help] [-v/--version ]<command> <arguments for the command, this can be chained infinite>

As one can see, there aren&rsquo;t really any options for yas.
99% of the people who use sudo (or opendoas), just use it with default configuration and the default options.
Who would also need a flag, to edit a file, if nobody ever uses that, and instead just runs \`sudo <editor> <file>\`


<a id="orgbc244a8"></a>

# Security

> You could have a car that is very safe by just limiting its
> max speed to 20 miles an hour. But I don&rsquo;t want to do that, I want to have
> something that&rsquo;s more like a Lamborghini, so maybe I&rsquo;ll throw in some airbags and
> it&rsquo;s gonna be mostly up to the driver to protect themselves and drive it safely.

Mental Outlaw on YouTube

Yas really doesn&rsquo;t try, and doesn&rsquo;t want to be the most secure option, but instead rather the fastest (as in no added security delay) or the **bloat free** option.

