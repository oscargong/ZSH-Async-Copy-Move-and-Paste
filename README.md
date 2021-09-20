# ZSH Async Copy Move and Paste

```zsh
# async copy
function ac() {
    unset ACOPY
    unset AMOVE
    export ACOPY=("${(@f)$(realpath -e $@)}")
}

# async move
function am() {
    unset ACOPY
    unset AMOVE
    export AMOVE=("${(@f)$(realpath -e $@)}")
}

# async paste
function ap() {
    if [ ! -z "$ACOPY" ]; then
        cp -vr "${ACOPY[@]}" .
    elif [ ! -z "$AMOVE" ]; then
        mv -v "${AMOVE[@]}" .
        unset AMOVE
    else
        >&2 echo "clipboard empty"
        return 1
    fi
}
```
