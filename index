
project=${PWD##*/}
org=$(git config --get remote.origin.url | grep -Eo "(\w*)/$project.git\/?$" | cut -d/ -f1)
platform=$(git config --get remote.origin.url | sed -e "s/[^/]*\/\/\([^@]*@\)\?\([^:/]*\).*/\2/")
branch=$(git branch | grep \* | cut -d ' ' -f2)
if [[ $org = *[!\ ]* ]]
then
    echo "Opening browsers..."
else
    echo "Not in repo"
    exit
fi

if [[ "$platform" == "bitbucket.org" ]]; then 
    url="https://${platform}/${org}/${project}/pull-requests/new?source=${branch}"
elif [[ "$platform" == "github.com" ]]; then
    url="https://${platform}/${org}/${project}/compare/master...${branch}"
elif [[ "$platform" == "gitlab.com" ]]; then
    url="https://${platform}/${org}/${project}/merge_requests/new?utf8=✓&merge_request%5B&merge_request%5Bsource_branch%5D=${branch}&merge_request%5B&merge_request%5Btarget_branch%5D=master"
else
    echo "Your git platform is not found."
    exit
fi
if [[ "$OSTYPE" == "linux-gnu" ]]; then
        xdg-open $url
elif [[ "$OSTYPE" == "darwin"* ]]; then
        open $url
elif [[ "$OSTYPE" == "cygwin" ]]; then
        cygstart $url
elif [[ "$OSTYPE" == "win32" ]]; then
        start $url
else
    echo "Your OS is not found."
    exit
fi