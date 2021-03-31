# Building emacs native on macOS 10.13

`brew install --build-from-source libgccjit` is required which took 4 hours for me.

This repository provides an `ansible` playbook to install the dependencies
required to compile `gccemacs` (native-compiled `emacs`) on OS X.

You must have `homebrew` and `ansible` installed to run these scripts.

```bash
python3 -m pip install ansible
```

To install the system dependencies, run

```bash
install-deps.sh
```

which, will run an `ansible` `playbook` that installs all of the system
dependencies.

Next, run

```bash
build.sh
```

to compile `gccemacs`.

Running `build.sh` creates `/Applications/Emacs-${TODAY}.app`, where `TODAY` is
an ISO-style date. You may use this application bundle or rename it to
`Emacs.app`. Running `build.sh` more than once per calendar day overwrites the
existing build.

## Check if native compilation works inside Emacs

From https://www.masteringemacs.org/article/speed-up-emacs-libjansson-native-elisp-compilation

```elisp
(if (and (fboundp 'native-comp-available-p)
       (native-comp-available-p))
  (message "Native compilation is available")
(message "Native complation is *not* available"))
```
