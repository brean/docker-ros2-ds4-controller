# docker-ros-ds4-controller
Example using docker-compose configuration to integrate the PlayStation Dual Shock 4-controller with ROS.

## Usage
1. install docker, docker-compose and terminator
1. build the docker container using docker-compose: `docker-compose build`
1. connect your Playstation Dual Shock 4 controller via USB or Bluetooth.
1. call the `run.bash`-script to start terminator with the two docker container.
1. move the stick of your controller. You see the published outtput of the ROS `/cmd_vel`-command on the right
1. once you close terminator the run.bash-script will stop the docker container by calling `docker-compose down`

<!--
TODO: how to change keyboard bindings?
TODO: more examples
TODO: integrate with ROS 2 turtlebot simulation?
-->
