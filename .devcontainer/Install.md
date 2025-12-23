# clone 

```
git clone --recurse-submodules https://github.com/coal-library/coal.git
git clone --recurse-submodules https://github.com/stack-of-tasks/pinocchio.git
git clone --recurse-submodules https://github.com/stack-of-tasks/eigenpy.git
git clone --recurse-submodules https://github.com/Gepetto/example-robot-data.git
git clone --recurse-submodules https://github.com/loco-3d/crocoddyl.git
git clone --recurse-submodules https://github.com/meshcat-dev/meshcat-python.git
```

# install meshcat-python, for visualization
```
cd src/meshcat-python
python3 -m pip install --user . --break-system-packages
```
# build crocoddyl (close unit test, and open python binding)
```
colcon build   --packages-up-to crocoddyl   --cmake-args -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTING=OFF -DBUILD_PYTHON_INTERFACE=ON -DBUILD_WITH_COLLISION_SUPPORT=ON -DCOAL_BACKWARD_COMPATIBILITY_WITH_HPP_FCL=ON
```
# run example
```
source install/setup.bash
```
```
cd src/crocoddyl/examples
python3 -m humanoid_taichi display
```
