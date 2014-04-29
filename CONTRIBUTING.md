# How to contribute to this project

Here's how I usually do when contributing to other people's projects, so it'll work for my own projects too:

* Fork the project
* Add the original project as the *upstream remote*
	
		git remote add upstream https://github.com/vokseverk/umbraco-xpath-guide.git
	
* Create a feature branch, e.g.:

		git checkout -b mntp

* Write your guide(s), committing locally along the way
* If you write for a long period of time, sync your fork with the upstream master:

		git checkout <your-branch-name>
		git fetch upstream
		git rebase upstream/master

* Push to your fork and create a pull-request on GitHub