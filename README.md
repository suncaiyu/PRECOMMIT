# PRECOMMIT
precommit



#!/bin/sh
# check file format

git diff --cached --name-only --diff-filter=ACMRT | grep "\.h$" | xargs -n1 clang-format -style=file -output-replacements-xml | grep "<replacement " >/dev/null
if [ $? -ne 1 ]
then 
    echo "Commit did not match clang-format！"
    exit 1;
fi
git diff --cached --name-only --diff-filter=ACMRT | grep "\.cpp$" | xargs -n1 clang-format -style=file -output-replacements-xml | grep "<replacement " >/dev/null
if [ $? -ne 1 ]
then 
    echo "Commit did not match clang-format！"
    exit 1;
fi
