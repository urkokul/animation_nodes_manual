*******************
Creating a new Node
*******************

A node is a single python file. All registration is done automatically.

At first you have to decide in which category your node idea fits.

    a) Choose one of the existing node categories (folders inside the ``nodes\\`` directory) or
    b) Create a new category. To do that make a new folder and put an empty file called ``__init__.py`` inside.

Then create a new python file inside the category you choosed and copy the template in:

    .. code-block:: python
        :linenos:

        import bpy
        from ... base_types.node import AnimationNode

        class TemplateNode(bpy.types.Node, AnimationNode):
            bl_idname = "an_TemplateNode"
            bl_label = "Template Node"

            def create(self):
                pass

            def execute(self):
                return

Replace *Template* with the name of your node.

    .. code-block:: python
        :linenos:

        class RoundNumberNode(bpy.types.Node, AnimationNode):
            bl_idname = "an_RoundNumberNode"
            bl_label = "Round Number"

Create the input and output sockets in the ``create`` function:

    .. code-block:: python
        :linenos:

        def create(self):
            self.inputs.new("an_FloatSocket", "Number", "number")
            self.inputs.new("an_IntegerSocket", "Decimals", "decimals")
            self.outputs.new("an_FloatSocket", "Rounded Value", "value")

    The parameters are:

        1. ``bl_idname`` of the socket type. You find all existing types here: :ref:`socket-data-types`
        2. Name of the socket that will be visible in the UI.
        3. Variable name that will be used in the ``execute`` function

Fill in the execution code:

    .. code-block:: python
        :linenos:

        def execute(self, number, decimals):
            value = round(number, decimals)
            return value

Save, start Blender test if your node works.
It isn't in the menu yet but you can find the node by searching for the ``bl_label`` property.


This is the final node file:

.. code-block:: python
    :linenos:

    import bpy
    from ... base_types.node import AnimationNode

    class RoundNumberNode(bpy.types.Node, AnimationNode):
        bl_idname = "an_RoundNumberNode"
        bl_label = "Round Number"

        def create(self):
            self.inputs.new("an_FloatSocket", "Number", "number")
            self.inputs.new("an_IntegerSocket", "Decimals", "decimals")
            self.outputs.new("an_FloatSocket", "Rounded Value", "value")

        def execute(self, number, decimals):
            value = round(number, decimals)
            return value
