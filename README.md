# git-service-desk

A git hook to automatically retrieve the title of your Service Desk record for your git feature branches.

## Installation

1. Get your API key from https://desk.gotoassist.com/my_api_token and put it in a file named
   <tt>~/.service_desk_api_token</tt>
2. Make sure the post-checkout file is executable (<tt>chmod +x</tt>)
3. Copy the post-checkout file into the .git/hooks directory of the relevant projects

## Using

If you're working on service desk record 12345, call your branch <tt>b12345</tt>.  As soon as you check it out, git-service-desk will pull down the title for the record and set it as your branch description.

You might want to use this handy piece of bash in your .profile for showing a list of your branches with descriptions beside them:

```bash
function gb() {
    branches=$(git for-each-ref --format='%(refname)' refs/heads/ | sed 's|refs/heads/||')
    for branch in $branches; do
        desc=$(git config branch.$branch.description)
        if [ $branch == $(git rev-parse --abbrev-ref HEAD) ]; then
            branch="* \033[0;32m$branch\033[0m"
        else
            branch="  $branch"
        fi
        echo -e "$branch \033[0;36m$desc\033[0m"
    done
}
```

## Credits

Credit to [@kuahyeow](https://github.com/kuahyeow) for the original idea and code.
