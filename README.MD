#AAAAA
This game is a proof of concept for us to use C in a game becuase we are masochist (or not), still, more important things following:
#Libraries used
- BGFX for Graphic Abstractions
- GLFW for Windowing 
- Chipmunk2D for Physics
- flecs for ECS
- cr for Plugin separation
- cuteheaders for a bunch of things (you can see in libs/single_header)
- hypathia for maths
- nuklear for UI
- log for logging internal stuff 
- mimalloc for memory allocation
- cmocka (Since someone wanted to unit test)
- CGet for dependency management
# Dependency Management
We use Cget to manage libraries (since I am stubborn af and I like it), so all the libraries are to be managed in the requirements.txt file for more info go to the [Cget repo](https://github.com/pfultz2/cget) or the [Cget Docs](https://cget.readthedocs.io/) 
# How to build the game
First run cget manager with the folowing command
```bash
cget install -p libs\cget
```
if all is right we should have populated the libs itself and we only have to do
```bash
mkdir build && cd build
cmake ..
```
And that should be all, the game should appear there