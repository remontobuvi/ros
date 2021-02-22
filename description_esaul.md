## Реализация гусениц
Гусеницы были реализованы как сочетание прямоугольного блока и колес
```bash
  <xacro:macro name="link_track" params="name">
    <link name="${name}">
      <collision name="collision_left_track">
        <origin rpy="0 0 0" xyz="0 0 0"/>
        <geometry>
          <box size="${box_length} ${box_width} ${box_height}"/>
        </geometry>
      </collision>
      <visual>
        <origin rpy="0 0 0" xyz="0 0 0"/>
        <geometry>
          <box size="${box_length} ${box_width} ${box_height}"/>
        </geometry>
        <material name="black"/>
      </visual>
      <xacro:solid_cuboid_inertial
            length="${box_length}" width="${box_width}"
            height="${box_height}" mass="${track_mass}">
        <origin xyz="0 0 0" rpy="0 0 0" />
      </xacro:solid_cuboid_inertial>
    </link>
    <gazebo reference="${name}">
      <mu1>0</mu1>
      <mu2>0</mu2>
      <material>Gazebo/Black</material>
    </gazebo>
  </xacro:macro>
  
    <xacro:macro name="link_wheel" params="name">
    <link name="${name}">
      <xacro:solid_cylinder_inertial
          r="${track_rad}" h="${track_length}"
          mass="${wheel_mass}" >
        <origin xyz="0 0 0" rpy="0 0 0" />
      </xacro:solid_cylinder_inertial>
      <collision name="link_right_wheel_collision">
        <origin rpy="0 1.5707 1.5707" xyz="0 0 0"/>
        <geometry>
          <cylinder length="${track_length}" radius="${track_rad}"/>
        </geometry>
      </collision>
      <visual name="${name}_visual">
        <origin rpy="0 1.5707 1.5707" xyz="0 0 0"/>
        <geometry>
          <cylinder length="${track_length}" radius="${track_rad}"/>
        </geometry>
      </visual>
    </link>
    <gazebo reference="${name}">
      <mu1>1.5</mu1>
      <mu2>1.5</mu2>
      <material>Gazebo/Black</material>
      <kp>10000000</kp>
      <kd>1</kd>
    </gazebo>
  </xacro:macro>
```
> Длина прямоугольного блока вычисляется таким образом, чтобы его края соединяли центры крайних колес, его толщина равна толщине колес, а высота должна равняться их диаметру. 

