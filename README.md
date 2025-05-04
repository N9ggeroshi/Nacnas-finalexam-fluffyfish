Nacnas, Kevin 3rd-year CIT Flappy Fish Game Documentation 
Overview 
Flappy Fish is a browser-based, single-player game inspired by Flappy Bird. The player 
controls a fish navigating through a series of pipes by making it "swim" (jump) to avoid 
collisions. The game features a start screen, game over screen, score tracking, audio effects, 
offline detection, and a 1.5-second delay before restarting after a game over. It is built using 
HTML5, JavaScript, and CSS, leveraging the HTML5 Canvas API for rendering. 
Key Features 
●  Gameplay: Navigate the fish through gaps between pipes using jump mechanics. 
●  Scoring: Earn 0.5 points for each pipe passed, displayed on-screen and on the game 
over screen. 
●  Audio: Background music loops during gameplay, with sound effects for jumping and 
game over. 
●  Offline Detection: Displays a message if the browser is offline, pausing gameplay. 
●  Restart Delay: A 1.5-second delay before restarting the game after a game over, 
triggered by any key or a restart button. 
●  Responsive UI: Start, game over, and offline screens with consistent styling. 
●  Controls: Space, Arrow Up, or X keys to jump; any key to start or restart. 
Setup Instructions 
Prerequisites 
●  A modern web browser (e.g., Chrome, Firefox, Safari). 
●  A local server (optional) to avoid CORS issues when loading assets (e.g., use 
http-server or a development server). 
●  Audio and image assets (see below). 
File Structure 
flappy-fish/ 
├── index.html          # Main HTML file 
├── flappyfish.js       # Game logic and rendering 
├── flappyfish.css      # Styling for UI elements 
├── background.jpg      # Canvas background image 
├── images.png          # Fish sprite 
├── toppipe.png         # Top pipe sprite 
├── bottompipe.png      # Bottom pipe sprite 
├── background.mp3      # Background music 
├── jump.mp3            # Jump sound effect 
├── gameover.mp3        # Game over sound effect 
 
Asset Requirements 
●  Images: 
○  background.jpg: Background image for the canvas (540x960 pixels 
recommended). 
○  images.png: Fish sprite (51x36 pixels). 
○  toppipe.png: Top pipe sprite (96x768 pixels). 
○  bottompipe.png: Bottom pipe sprite (96x768 pixels). 
●  Audio: 
○  background.mp3: Looping background music (MP3 format, seamless loop 
preferred). 
○  jump.mp3: Sound effect for fish jumping. 
○  gameover.mp3: Sound effect for game over. 
●  Assets must be placed in the same directory as index.html. Source royalty-free 
assets from sites like Freesound or Incompetech (ensure proper licensing). 
Running the Game 
1.  Place all files in a directory. 
2.  Ensure assets are correctly named and located. 
3.  Open index.html in a browser: 
○  Directly via file:// (may have CORS issues with audio/images). 
○  Preferably, use a local server (e.g., npx http-server or VS Code Live 
Server). 
4.  The start screen will appear. Press the "Start Game" button or any key to begin. 
Gameplay Mechanics 
Objective 
Guide the fish through gaps between pairs of pipes without colliding. The game ends if the fish 
hits a pipe or falls off the screen. 
Controls 
●  Jump: Press Space, Arrow Up, or X to make the fish jump (applies upward velocity). 
●  Start Game: Click the "Start Game" button or press any key on the start screen. 
●  Restart Game: During game over, press any key or click the "Restart" button. A 
1.5-second delay occurs before the game resets. 
Game States 
●  Start Screen: Displays game instructions and a start button. Hidden once the game 
begins. 
●  Gameplay: The fish moves forward automatically; the player controls vertical movement. 
Pipes spawn every 1.5 seconds. 
●  Game Over: Triggered by hitting a pipe or falling off the screen. Shows the final score 
and a restart button. A 1.5-second delay precedes restarting. 
●  Offline: If the browser is offline, an offline screen appears, and gameplay is paused. 
Scoring 
●  The score increases by 0.5 for each pipe the fish passes (when the fish's x-coordinate 
exceeds the pipe's right edge). 
●  Displayed in white, 67px sans-serif font at the top-left corner during gameplay. 
●  Shown on the game over screen as "Your Score: [score]". 
Audio 
●  Background Music: Loops during gameplay, pauses on game over or offline state, 
resumes on start/restart. 
●  Jump Sound: Plays when the fish jumps (Space, Arrow Up, or X pressed). 
●  Game Over Sound: Plays when the fish collides with a pipe or falls. 
Code Structure 
index.html 
●  Purpose: Defines the game’s HTML structure. 
●  Key Elements: 
○  <canvas id="board">: The game rendering area (540x960 pixels). 
○  <div id="startScreen">: Start screen with instructions and a start button. 
○  <div id="gameOverScreen">: Game over screen with final score and restart 
button. 
○  <div id="offlineScreen">: Offline message screen. 
○  <audio> elements: For background music (backgroundMusic), jump sound 
(jumpSound), and game over sound (gameOverSound). 
●  Scripts/Styles: Links flappyfish.js and flappyfish.css. 
flappyfish.js 
●  Purpose: Handles game logic, rendering, and event handling. 
●  Key Variables: 
○  board, context: Canvas and 2D rendering context. 
○  bird: Object with position (x, y), size (width, height), and sprite (birdImg). 
○  pipeArray: Array of pipe objects (top and bottom pipes with position, size, 
sprite, and passed flag). 
○  velocityX, velocityY, gravity: Physics parameters for pipe movement and 
fish falling/jumping. 
○  gameOver, gameStarted, score: Game state and score tracking. 
○  backgroundMusic, jumpSound, gameOverSound: Audio elements. 
○  isOnline: Tracks internet connectivity. 
○  isRestarting: Prevents multiple restarts during the 1.5-second delay. 
●  Key Functions: 
○  window.onload: Initializes canvas, loads images/audio, sets up event listeners, 
and starts the game loop. 
○  update: Main game loop (via requestAnimationFrame). Clears canvas, 
updates game state, renders objects, and handles game over/offline states. 
○  placePipes: Spawns top and bottom pipes every 1.5 seconds with a random 
gap. 
○  moveBird: Handles key presses for jumping, starting, or restarting. 
○  startGame: Starts the game, hides the start screen, and plays background 
music. 
○  restartGame: Resets the game state after a 1.5-second delay and resumes 
music. 
○  detectCollision: Checks for collisions between the fish and pipes. 
○  updateOnlineStatus: Toggles offline screen and pauses music when 
connectivity changes. 
flappyfish.css 
●  Purpose: Styles the game’s UI elements. 
●  Key Styles: 
○  body: Centers the canvas and sets a light gray background. 
○  #board: Applies the background image (background.jpg). 
○  #startScreen, #gameOverScreen, #offlineScreen: Semi-transparent, 
centered overlays (400x400 pixels) with white text and rounded corners. 
○  #startButton, #restartButton: Styled buttons with hover effects. 
○  Fonts: Uses sans-serif for UI elements, with Courier New for the body. 
Technical Details 
Technologies 
●  HTML5: For structure and canvas/audio elements. 
●  JavaScript: For game logic, rendering, and event handling. 
●  CSS: For styling UI components. 
●  HTML5 Canvas API: For rendering the fish, pipes, score, and background. 
●  Web Audio API: For playing background music and sound effects. 
●  Navigator API: For detecting online/offline status (navigator.onLine). 
Physics 
●  Fish Movement: 
○  Horizontal: Fixed position (x = boardWidth/8). 
○  Vertical: Affected by gravity (gravity = 0.4) and jump velocity (velocityY = 
-6 on jump). Clamped to prevent moving above the canvas top. 
○  Game over if y > boardHeight. 
●  Pipe Movement: 
○  Spawn at x = boardWidth, move left at velocityX = -2 pixels per frame. 
○  Random vertical position with a fixed gap (board.height/4). 
Event Handling 
●  Keyboard: keydown event for jumping (Space, Arrow Up, X), starting, or restarting. 
●  Mouse: Click events on startButton and restartButton. 
●  Network: online/offline events to update connectivity status. 
Performance 
●  Uses requestAnimationFrame for smooth 60 FPS rendering. 
●  Clears unused pipes (pipeArray.shift()) to optimize memory. 
●  Pauses game updates during game over/offline states to reduce CPU usage. 
Limitations 
●  Asset Dependency: Requires specific image and audio files; missing assets cause 
rendering/audio issues. 
●  CORS Issues: Loading assets via file:// may fail in some browsers. Use a local 
server for testing. 
●  Mobile Support: Not optimized for touch input (e.g., tap to jump). 
●  Audio Volume: No volume controls; audio may be too loud/soft depending on files used. 
Potential Improvements 
●  Add touch support for mobile devices (tap to jump). 
●  Include a mute button or volume slider for audio. 
●  Display a countdown timer during the 1.5-second restart delay. 
●  Add high score tracking (e.g., using localStorage). 
●  Implement difficulty scaling (e.g., faster pipes over time). 
●  Enhance offline mode to allow gameplay with cached assets. 
Troubleshooting 
●  Assets Not Loading: 
○  Check file paths and names in index.html and flappyfish.js. 
○  Use a local server to avoid CORS issues. 
●  Audio Not Playing: 
○  Ensure MP3 files are valid and supported by the browser. 
○  Check browser console for errors (e.g., Failed to load resource). 
●  Game Not Starting/Restarting: 
○  Verify internet connectivity (offline mode blocks actions). 
○  Ensure no JavaScript errors in the console. 
●  Restart Delay Issues: 
○  Confirm isRestarting flag prevents multiple restarts. 
○  Test with different browsers to ensure setTimeout behaves consistently. 
Credits 
●  Developed by: [Your Name or "Anonymous" if not specified] 
●  Assets: Provide credits for image/audio assets if sourced from third parties (e.g., 
Freesound, Incompetech). 
●  Inspired by: Flappy Bird 
License 
This game is provided as-is for educational purposes. Ensure all assets used are properly 
licensed for your use case (e.g., Creative Commons for audio/images). 
 
Last Updated: May 02, 2025 
 
