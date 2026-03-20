from ursina import *

app = Ursina()

# Create ground
ground = Entity(
    model='plane',
    texture='white_cube',
    texture_scale=(20,20),
    scale=20,
    collider='box'
)

# Player
player = FirstPersonController()

# Block class
class Voxel(Button):
    def __init__(self, position=(0,0,0)):
        super().__init__(
            parent=scene,
            position=position,
            model='cube',
            origin_y=0.5,
            texture='white_cube',
            color=color.random_color(),
            scale=1
        )

    def input(self, key):
        if self.hovered:
            if key == 'left mouse down':
                Voxel(position=self.position + mouse.normal)
            if key == 'right mouse down':
                destroy(self)

# Generate some blocks
for z in range(10):
    for x in range(10):
        Voxel(position=(x,0,z))

app.run()
