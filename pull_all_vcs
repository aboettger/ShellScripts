#!/bin/bash -
#===============================================================================
#
#          FILE: pull_all_vcs
#
#         USAGE: ./pull_all_vcs
#
#   DESCRIPTION:
#
#       OPTIONS: ---
#  REQUIREMENTS: ---
#          BUGS: ---
#         NOTES: ---
#        AUTHOR: andreas.boettger@gmx.de
#  ORGANIZATION:
#       CREATED: Do 24 Apr 2014 12:38:05 CEST
#      REVISION:  ---
#===============================================================================

# set -o nounset                              # Treat unset variables as an error

if [ "$(command -v jshon)" == "" ]
then
  echo "jshon not installed. Aborting."
  exit 1
fi

rootDir="$HOME"
if [ "$1" != "" ]
then
  rootDir=$(realpath "$1")
fi

red='\e[0;31m'
green='\e[0;32m'
yellow='\e[0;33m'
NC='\e[0m' # No Color

# JSON
# replace \" with " and paste it here: http://www.jsoneditoronline.org/
rc="{\"GIT\":{\"name\":\"GIT\",\"command\":\"git\",\"pullSubCommand\":\"pull\",\"dotFolder\":\".git\"},\"SVN\":{\"name\":\"SVN\",\"command\":\"svn\",\"pullSubCommand\":\"update\",\"dotFolder\":\".svn\"},\"HG\":{\"name\":\"Mercurial\",\"command\":\"hg\",\"pullSubCommand\":\"pull\",\"dotFolder\":\".hg\"},\"BZR\":{\"name\":\"Bazaar\",\"command\":\"bzr\",\"pullSubCommand\":\"pull\",\"dotFolder\":\".bzr\"}}"

for vcr in $(echo "$rc" | jshon -k)
do
  command=$(echo "$rc" | jshon -e "$vcr" -e "command" | tr -d "\"")
  name=$(echo "$rc" | jshon -e "$vcr" -e "name" | tr -d "\"")
  dotFolder=$(echo "$rc" | jshon -e "$vcr" -e "dotFolder" | tr -d "\"")
  pullSubCommand=$(echo "$rc" | jshon -e "$vcr" -e "pullSubCommand" | tr -d "\"")
  if [ "$(command -v "$command")" == "" ]
  then
    echo -e "${red}$command not installed${NC}"
  else
    echo -e "${green}***** Checking $name repositories in ${yellow}$rootDir${NC}"
    echo
    find "$rootDir" -type d -name "$dotFolder" | sort | while read line; do
      workingDir=$(dirname "$line")
      echo -e "${green}$name: ${NC}${yellow}$workingDir${NC}"
      cd "$workingDir"
      echo -e "${green}$("$command" "$pullSubCommand")${NC}"
      echo
    done
  fi
done

exit 0

