all of the tasks that a developer does are able to be automated to some extent

# Best Practice
- automate everything (one-step build)
- always use a build tool
- Use CI to build and test your code on every commit
- dont depend on anything thats not in the build file (hermetic)!
- dont break the build!

# Build Systems 
use dependencies between tasks 

## Topological Search
- using trees to perform search as dependencies are non-linear 

# Gradle
open source successor to ant and maven
- groovy/kotlin dsl (vs.xml)
- many defaults for (maven) conventions
- can query maven central for dependency resolution 

# Poetry
python build tool
- builds python code into a tar.gz file
- also creates a "wheel" or a file with build instructions and dependency information 
- when built, also creats a .egg-info folder with sources and dependency links



