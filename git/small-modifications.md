# Small modifications

## Modify editor to subline

1. [Install Subline Text using snap](https://snapcraft.io/sublime-text)
2. Add to Sublime text package [GitSavvy](https://packagecontrol.io/packages/GitSavvy)
3. Set global config, running `git config --global core.editor "subl -n -w"` updates the `~/.gitconfig` file.

## Fast forwarding

More information [see](https://blog.sffc.xyz/post/185195398930/why-you-should-use-git-pull-ff-only-git-is-a), [more options include merge](https://stackoverflow.com/questions/2500296/can-i-make-fast-forwarding-be-off-by-default-in-git)

 1. `git config --global pull.ff`
 2. `git config --global merge.ff` (not create an extra merge commit when merging a commit, this is also the default)
    * `git config  --global  branch.master.mergeoptions  "--no-ff"`
    * `git config  --global  branch.main.mergeoptions  "--no-ff"`
 3. Reconfigure the PS1

    ```bash
    # Reset
    Color_Off="\[\033[0m\]"       # Text Reset

    # Regular Colors
    Black="\[\033[0;30m\]"        # Black
    Red="\[\033[0;31m\]"          # Red
    Green="\[\033[0;32m\]"        # Green
    Yellow="\[\033[0;33m\]"       # Yellow
    Blue="\[\033[0;34m\]"         # Blue
    Purple="\[\033[0;35m\]"       # Purple
    Cyan="\[\033[0;36m\]"         # Cyan
    White="\[\033[0;37m\]"        # White

    # Bold
    BBlack="\[\033[1;30m\]"       # Black
    BRed="\[\033[1;31m\]"         # Red
    BGreen="\[\033[1;32m\]"       # Green
    BYellow="\[\033[1;33m\]"      # Yellow
    BBlue="\[\033[1;34m\]"        # Blue
    BPurple="\[\033[1;35m\]"      # Purple
    BCyan="\[\033[1;36m\]"        # Cyan
    BWhite="\[\033[1;37m\]"       # White

    # Define color codes for better readability
    RED='\[\e[0;31m\]'
    GREEN='\[\e[0;32m\]'
    BLUE='\[\e[0;34m\]'
    YELLOW='\033[1;33m'
    ORANGE='\033[0;33m'
    WHITE='\033[1;37m'
    NO_COLOR='\[\e[0m\]'  # Reset color

    # Function to display Git branch and status if in a Git repository
    update_ps1_with_git_info() {
        # Check if we're inside a Git repository
        if git rev-parse --is-inside-work-tree &>/dev/null; then
        # Get the current branch name
        local git_branch=$(git branch 2>/dev/null | grep '*' | sed 's/* //')
        # Check if there are uncommitted changes
        local git_dirty=$(git status --porcelain 2>/dev/null | wc -l)
        local git_status=""
                
        # If there are uncommitted changes, show "~modified"
        if [ "$git_dirty" -ne 0 ]; then
            git_status="${BGreen}~${WHITE}modified${NO_COLOR}"
            fi

            local git_pwd_info="${BRed}(${git_branch}${git_status}${BRed})${NO_COLOR}"
            # Update PS1 to include Git info
            PS1="${ORIGINAL_PS1%\\$ }${git_pwd_info}${NO_COLOR}$ "
        else
            # If not in a Git directory, use the original PS1
            PS1="${ORIGINAL_PS1}"
        fi
    }

    # Save the original PS1 so we can restore it when not in a Git directory
    ORIGINAL_PS1="$PS1"

    # Hook the update_ps1_with_git_info function to PROMPT_COMMAND
    export PROMPT_COMMAND="update_ps1_with_git_info; $PROMPT_COMMAND"
    ```

    * Explanation, `${ORIGINAL_PS1%\\$ }` This removes the final `$` from the original prompt temporarily. It allows you to replace it with the Git branch information and `$`
