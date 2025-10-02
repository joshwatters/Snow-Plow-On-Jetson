# Autonomous Snowplow
## About SnowPlow


Autonomous Snowplow:  Autonomous Snowplow is tasked with clearing a predetermined area of snow without any human input; we can only use algorithms, computer vision, and additional sensors. We recently rebuilt the drive train.

Previous Competition Website: http://www.autosnowplow.com/welcome.html

Previous Design: https://www.youtube.com/watch?v=uQ3A9CB2F4g

Project Overview: [Project Overview](./Docs/overview.MD)

### Documentation and resources

  Documentation for implementation of Isaac Lab can be found at:
  https://docs.isaacsim.omniverse.nvidia.com/latest/installation/quick-install.html
  
  While documentation for standard Isaac Sim can be seen at:
  https://docs.isaacsim.omniverse.nvidia.com/latest/robot_simulation/index.html
  
## Snow Plow features

- most functionality can be viewed within the scripts contained in the [src](./src) folder.
- For simplicity singular programming language "Python" was used for the program itself.
- C++ was added for sensor package functionality to allow for arduino code-reusability (Examples included).
- Code has been internally commented for ease of use.

## Usage

If you have GIT configured, quickly deploy using `cmd`:

```bash
git clone https://github.com/ISURobotics/SnowPlow25/
```

```bash
$ git clone https://github.com/ISUrobotics/SnowPlow25/
> Cloning into `Folder`...
> remote: Counting objects: 10, done.
> remote: Compressing objects: 100% (8/8), done.
> remove: Total 10 (delta 1), reused 10 (delta 1)
> Unpacking objects: 100% (10/10), done.
```

## Snow-Plow-On-Jetson
Repository to be cloned directly to the Jetson Nano on the autonomous Snow Plow Project
In the event of a catastrophic failure and a complete reinstall is nessecary, see:
- [Reinstall](/Docs/reinstall.MD)

For general operating procedures, see:
- [Operating Procedure](/Docs/operating.MD)
- [Lidar](/Docs/lidar.MD)
## Releases

**The README for the `1.x` version is on the [v1.x](./tree/v1.x) branch.**
