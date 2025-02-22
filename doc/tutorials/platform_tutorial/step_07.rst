.. _platformer_part_seven:

Step 7 - Adding a Camera
------------------------

Now that our player can move and jump around, we need to give them a way to explore the world
beyond the original window. If you've ever played a platformer game, you might be familiar with the
concept of the screen scrolling to reveal more of the map as the player moves.

To achieve this, we can use a Camera, Arcade provides :class:`arcade.SimpleCamera` and :class:`arcade.Camera`.
They both do the same base thing, but Camera has a bit of extra functionality that SimpleCamera doesn't.
For now, we will just use the SimpleCamera.

To start with, let's go ahead and add a variable in our ``__init__`` function to hold it:

.. code-block::

    self.camera = None

Next we can go to our setup function, and initialize it like so:

.. code-block::

    self.camera = arcade.SimpleCamera(viewport=(0, 0, self.width, self.height))

The ``viewport`` parameter here defines the size of the camera. In most circumstances, you will want this
to be the size of your window. So we specify the bottom and left coordinates of our camera viewport as
(0, 0), and provide it the width and height of our window.

In order to use our camera when drawing things to the screen, we only need to add one line to our ``on_draw``
function. This line should typically come before anything you want to draw with the camera. In later chapters,
we'll explore using multiple cameras to draw things in different positions. Go ahead and add this line before
drawing our SpriteLists

.. code-block::

    self.camera.use()

If you run the game at this point, you might notice that nothing has changed, our game is still one static un-moving
screen. This is because we are never updating the camera's position. In our platformer game, we want the camera to follow
the player, and keep them in the center of the screen. Arcade provides a helpful function to do this with one line of code.
In other types of games or more advanced usage you may want to set the cameras position directly in order to create interesting
effects, but for now all we need is the ``center()`` function of our camera.

If we add the following line to our ``on_update()`` function and run the game, you should now see the player
stay at the center of the screen, while being able to scroll the screen around to the rest of our map. For fun, see what happens
if you fall off of the map! Later on, we'll revisit a more advanced camera setup that will take the bounds of our world into
consideration.

.. code-block::

    self.camera.center(self.player_sprite.position)

Source Code
~~~~~~~~~~~

.. literalinclude:: ../../../arcade/examples/platform_tutorial/07_camera.py
    :caption: Adding a Camera
    :linenos:
    :emphasize-lines: 49-50, 96-97, 107-108, 120-121

Run This Chapter
~~~~~~~~~~~~~~~~

.. code-block::

  python -m arcade.examples.platform_tutorial.07_camera
