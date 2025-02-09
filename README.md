**Note that it throws an `emacs: dlopen(/usr/local/bin/../native-lisp/28.0.50-e3916d16/window-0d1b8b93-513ac8ca.eln, 1): image not found` error now for some reason although it worked previously :(**

---

`brew install --build-from-source libgccjit` is required which took 4 hours for me.

`no-titlebar.patch` needs to be applied manually after cloning the repository.

---

### Building Emacs native for macOS 10.13 (and possibly later)

This repository provides an `ansible playbook` to install the dependencies
required to compile `gccemacs` (native-compiled `emacs`) on macOS.

You must have `homebrew` and `ansible` installed to run these scripts.

```bash
python3 -m pip install ansible
```

To install the system dependencies via an `ansible playbook` run:

```bash
sh install-deps.sh
```

`build.sh` compiles `gccemacs` and outputs `Emacs.app` which takes about 90 minutes for me.

Running `build.sh` creates `/Applications/Emacs-${TODAY}.app`, where `TODAY` is
an ISO-style date. You may use this application bundle or rename it to
`Emacs.app`. Running `build.sh` more than once per calendar day overwrites the
existing build.

```bash
sh build.sh
```

## Check if native compilation works inside Emacs

From https://www.masteringemacs.org/article/speed-up-emacs-libjansson-native-elisp-compilation

```elisp
(if (and (fboundp 'native-comp-available-p)
       (native-comp-available-p))
  (message "Native compilation is available")
(message "Native complation is *not* available"))
```
