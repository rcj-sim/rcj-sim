# The rcj-sim Project
rcj-sim is a project to develop a simulation for the [RoboCup Junior
Soccer](https://junior.robocup.org/soccer/) league.

## State of the project
This project is in an early planning and evaluation phase.
I published it early because I make references to it in a letter of
motivation.
Also, this opens up great possibilities of discussion with future users
and other people interested in contributing.

There is already a small prototype that I use for experimenting with the
physics engine, Bullet, and OpenSceneGraph in the submodule `mockup`.

## Building
If you run into trouble because the libraries in your distribution do
not have version numbers that are high enough, please lower the version
numbers in the `libs/CMakeLists.txt` and try out whether it your version
of the library works.
Currently, this is more likely than not.
If it does, create a pull request to lower the version numbers.

I did not test whether this can be built on Windows, but if you get it to
work, please create a pull request with your changes.

## Dependencies
rcj-sim requires a recent compiler supporting at least the C++17 standard.
It also requires [CMake](https://cmake.org) as its build system.
It depends on [Bullet](https://pybullet.org/wordpress/) as a physics
library and [OpenSceneGraph](http://www.openscenegraph.org/) for graphics
abstraction.
Both of these libraries are contained in the repository as git
subprojects.
It is recommended that you build these libraries yourselves, so that the
version numbers match.
However, you can also use pre-packaged versions from your OS distribution.
To build OpenSceneGraph from source, you also need OpenGL >= 3.1 and the
corresponding header files installed.
OpenSceneGraph has some more dependencies, install these as needed.
CMake will tell you what is missing.

On a freshly installed Debian Buster, I had to install these packages:
- `git` for checking out the project.
- `cmake` for configuration.
- `clang` as a C++ compiler. `g++` will work, too, if you have that
	installed.
- `libgl-dev` as a dependency of OpenSceneGraph.
So, for example, do
```
apt install git cmake clang libgl-dev
```


### Build instructions
- Clone/Download the repository.
- Initialize git submodules: On the shell, do
    ```
    git submodule update --init --depth 1
    ```
- Create a directory `build`.
    In-source builds are not officially supported.
    ```
    mkdir build
    ```
- Change to that directory and on the shell, run `cmake ..`.
    This will configure the build.
    ```
    cd build
    cmake ..
    ```
    There are some build options which are not documented yet.
- Then, as usual, run `make`.
    ```
    make
    ```

## License
This program is free software:
you can redistribute it and/or modify it under the terms of the GNU Affero
General Public License as published by the Free Software Foundation,
either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but
WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY
or FITNESS FOR A PARTICULAR PURPOSE.
See the GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program.
If not, see <https://www.gnu.org/licenses/>.
