# DESIGN Document

### Yasha Doddabele, Nikita Daga, Arnav Nayak, Philip Lee, Divyansh Jain, Joseph Ogunbadewa, Jonathan Esponda

## Team Roles and Responsibilities

* Team Member #1 (Philip Lee)
    * Responsible for the rule interpreter, strategy and visitor pattern that assigns strategies to
      corresponding blocks.
    * Worked on controllers such as GameState controller which is responsible for winning and losing
      logic.
    * Also developed the social center and leaderboard by creating database connections and classes
      to interact with the MongoDB Atlas interface.

* Team Member #2: (Yasha Doddabele)
    * Responsible for front-end gameplay, entrypoint, making all the images/UI/widget
      factory, and making the properties files for languages
    * Created the GameGridObserver, implemented the Observer paradigm in the Gameplay view

* Team Member #3: (Joseph Ogunbadewa)
    * Responsible for the movement of blocks in the grid, which handles the data structure that is
      read by the view
    * Handled the interpretation of key presses on the game player back end
    * Developed the Artificial player extension

* Team Member #4 (Nikita Daga)
    * Responsible for the authoring environment view
    * Worked on the block viewing scroll pane and categorization of blocks here. Also worked on
      allowing grid size changes, and adapting the drag and drop functionality to align with new
      grids. Was also responsible for creating level validations when saving.

* Team Member #5 (Divyansh Jain)
    * Responsible for the front end of the authoring environment
    * Worked on core drag and drop functionality, remove blocks functionality, help system (hover
      and dialog box), saving and loading of files from authoring environment, error handling for
      grid size, cheat keys and resource bundles.
    * Also helped with the overall loading functionality/debugging, adding methods to
      levelcontroller, Grid and JSONLoader classes.

* Team Member #6 (Jonathan Esponda)
    * Responsible for JsonManager class and the loading and saving of different games and levels.
    * Helped initially with the view of the game player and also helped with the authoring
      environment model.

## Design Goals

* Goal #1
    * We wanted to create a game engine that could adapt to new blocks easily. As such, we created a
      block factory that could create new blocks based on their type and category, as well as
      implemented a visitor pattern to assign strategies to blocks with minimal code changes.

* Goal #2
    * Design is intuitive, neat, and standardized
    * No hardcoded values in the view, so almost all widget text are located in property files
    * UI widgets are shared between the two environments

* Goal #3
    * We wanted the authoring environment and game player to be well-connected with a process to
      save from the authoring environment and load it into the game player, whilst also being able
      to do the reverse. This was important in being able to take an existing level and editing it
      in the authoring environment.

#### How were Specific Features Made Easy to Add

* Feature #1: Adding a new block to the game engine and making it work with attributes was made easy
  by block factory and visitor pattern. The block factory could create new blocks based on their
  type and
  category, and the visitor pattern could assign strategies to blocks with minimal code changes.

* Feature #2: It's easy to add new languages. Simply add the language name as a parameter to a combo
  box, then make a properties file with all necessary texts/buttons converted to the language you
  want.

* Feature #3: It is easy to add new blocks and their categories to the authoring view since all
  of this information is read from a json file. Only the file needs to be updated for new blocks and
  one line of code for new category types.

## High-level Design

#### Core Classes and Abstractions, their Responsibilities and Collaborators

* Class #1
    * A core class was the rule interpreter which was responsible for interpreting the rules of the
      game. This class was important in the gameplay as it was responsible for interpreting the
      rules of the game and applying them to the blocks on the grid. It was abstracted as it
      followed
      single responsibility, and was only used to assign strategies to blocks.

* Class #2
    * Core abstraction: Scene interface (and all Scene classes)
    * The Scene interface is helped to standardize View-related classes. All high level view classes
      like MainScene implement the Scene interface, and they are all managed by a SceneController
      class.
    * For more complex functionality, classes within scenes are split into Panes (aka, MainScene
      contains the GamePane and InteractionPane) to follow the multiple classes' principle.


* Class #3
    * A core class for out game is the Grid class. this handles the movement of blocks in the grid
      and defines all the public methods that other classes call to interact with the grid.
    * Another core class is the KeyHandler abstraction, which is extended by all the keyhandler
      classes (LeftKeyHandler, RightKeyHandler, UpKeyHandler, DownKeyHandler, EnemyKeyHandler). It
      defines the way that each of these key presses should modify the grid.

* Class #4
    * A core class for our project was the JsonManager class. This class was an example of the
      facade design pattern as it was created to encapsulate the GSON library that we used to be
      able to handle our json files. This class was important in the parsing of levels to json and
      vice versa, whilst also being important to the level controllers being able to save and load.

 