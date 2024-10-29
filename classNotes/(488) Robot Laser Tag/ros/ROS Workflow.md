# Project directory
in general, there are 3 main directories which you need to be aware of. These exist inside the directory which will house your entire catkin environment and ROS project:
- build
- devel
- src 

you may have to do a simple `$dir src` to create the src folder but after that, given that you've installed ros and catkin correctly, you just need to run `catking_make` - this will produce the build and devel folders. **NOTE: ALWAYS EXECUTE CATKIN_MAKE INSIDE THE `src` FOLDER - NEVER OUTSIDE OF IT**

# Project Package Creation 
in order to create your own package for your particular project, navigate into the `/src` directory and run the following command 
```shell
catkin_create_pkg my_pkg_name dependency1 depedency2...
```
- make sure to use lowercase for your project package name 

### A Note on adding or Correcting incorrectly declared dependencies 
if you incorrectly declare a dependency (i.e. type in the name wrong) there is a way to fix it. First, open the package directory that you just created. Along with the `src/` file, you should see:
- `package.xml`

### Editing `package.xml` 
within this file, you should see the names of all your packages between the following carrot blocks:
- `<build_depend></build_depend>`
- `>exec_depend></exec_depend>`
just edit the package names in between those blocks to the correct names and save 


# Setting up `~/.bashrc` to have each shell setup for running ROS
at the very bottom of your `.bashrc` you must source the setup script for your custom project package. this is done with 
```bash
source ~/workspace/location/path/devel/setup.bash 
```
- this will run the setup script every time you open up a new terminal and is necessary to prepare the environment for ROS

