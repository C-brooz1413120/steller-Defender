
import React, { useEffect, useRef, useState } from 'react';
import { PowerOff, ArrowUp, ArrowDown, ArrowLeft, ArrowRight, Heart, Play, RotateCcw, Home, Pause } from 'lucide-react';

export default function StellarDefender() {
  const canvasRef = useRef(null);
  const gameRef = useRef(null);
  const audioRef = useRef(null);
  const [gameState, setGameState] = useState('menu'); // menu, playing, paused, gameOver
  const [score, setScore] = useState(0);
  const [lives, setLives] = useState(3);
  const [highScore, setHighScore] = useState(0);
  const [isTouchDevice, setIsTouchDevice] = useState(false);
  const [deviceType, setDeviceType] = useState('desktop'); // mobile, tablet, desktop

  useEffect(() => {
    const checkDevice = () => {
      const width = window.innerWidth;
      const isTouchCapable = 'ontouchstart' in window || navigator.maxTouchPoints > 0;
      
      if (isTouchCapable && width < 768) {
        setDeviceType('mobile');
        setIsTouchDevice(true);
      } else if (isTouchCapable && width >= 768 && width < 1024) {
        setDeviceType('tablet');
        setIsTouchDevice(true);
      } else {
        setDeviceType('desktop');
        setIsTouchDevice(false);
      }
    };

    checkDevice(); // Initial check
    window.addEventListener('resize', checkDevice); // Listen for resize to update device type
    
    const canvas = canvasRef.current;
    if (!canvas) return;

    // --- Correctly lock the viewport without breaking buttons ---
    const preventDefault = (e) => e.preventDefault();
    document.body.style.overflow = 'hidden';
    document.addEventListener('touchmove', preventDefault, { passive: false });
    
    let viewport = document.querySelector("meta[name=viewport]");
    if (!viewport) {
      viewport = document.createElement('meta');
      viewport.name = 'viewport';
      document.head.appendChild(viewport);
    }
    viewport.content = 'width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, shrink-to-fit=no';
    
    // --- Load Data and Initialize ---
    const savedData = localStorage.getItem('stellarDefenderData');
    if (savedData) {
      const data = JSON.parse(savedData);
      setHighScore(data.highScore || 0);
    }

    initializeAudio();

    gameRef.current = new StellarDefenderGame(canvas, {
      onScoreUpdate: setScore,
      onLivesUpdate: setLives,
      onGameOver: () => setGameState('gameOver'),
      playSound: playSound,
      deviceType: deviceType // Pass deviceType to game engine
    });

    const handleResize = () => gameRef.current?.resize();
    window.addEventListener('resize', handleResize);
    handleResize(); // Initial resize for canvas

    return () => {
      // Cleanup
      window.removeEventListener('resize', handleResize);
      window.removeEventListener('resize', checkDevice); // Clean up device check listener
      document.removeEventListener('touchmove', preventDefault);
      document.body.style.overflow = 'auto';
      gameRef.current?.destroy();
    };
  }, [deviceType]); // Re-run effect if deviceType changes to update gameRef with new deviceType

  const initializeAudio = () => {
    if (typeof window !== 'undefined' && (window.AudioContext || window.webkitAudioContext)) {
      audioRef.current = { context: new (window.AudioContext || window.webkitAudioContext)() };
    }
  };

  const playSound = (type) => {
    // Only play shooting sound
    if (type !== 'shoot') return;
    
    if (audioRef.current?.context) {
      try {
        const audioContext = audioRef.current.context;
        const oscillator = audioContext.createOscillator();
        const gainNode = audioContext.createGain();
        oscillator.connect(gainNode);
        gainNode.connect(audioContext.destination);

        // Shooting sound
        oscillator.type = 'triangle';
        oscillator.frequency.setValueAtTime(800, audioContext.currentTime);
        oscillator.frequency.exponentialRampToValueAtTime(400, audioContext.currentTime + 0.1);
        gainNode.gain.setValueAtTime(0.08, audioContext.currentTime);
        gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.1);
        
        oscillator.start(audioContext.currentTime);
        oscillator.stop(audioContext.currentTime + 0.1);
      } catch (e) {
        console.error("Could not play sound", e);
      }
    }

    // Vibration feedback on touch devices for shooting only
    if (isTouchDevice && navigator.vibrate) {
      navigator.vibrate(30);
    }
  };

  const startGame = () => {
    setGameState('playing');
    setScore(0);
    setLives(3);
    gameRef.current?.start();
  };

  const pauseGame = () => {
    setGameState('paused');
    gameRef.current?.pause();
  };

  const resumeGame = () => {
    setGameState('playing');
    gameRef.current?.resume();
  };

  const restartGame = () => {
    setGameState('playing');
    setScore(0);
    setLives(3);
    gameRef.current?.start();
  };

  const returnToMenu = () => {
    setGameState('menu');
    gameRef.current?.stop();
  };

  const saveGame = () => {
    const currentHighScore = Math.max(score, highScore);
    localStorage.setItem('stellarDefenderData', JSON.stringify({ highScore: currentHighScore }));
    setHighScore(currentHighScore);
  };
  
  const handleExit = () => {
    window.location.href = 'https://games.gamebin.online';
  };

  useEffect(() => {
    if (gameState === 'gameOver' || gameState === 'menu') {
      saveGame();
    }
  }, [gameState, score, highScore]);

  // Responsive classes based on device type
  const getResponsiveClasses = () => {
    switch (deviceType) {
      case 'mobile':
        return {
          title: 'text-4xl sm:text-5xl',
          subtitle: 'text-2xl sm:text-3xl',
          button: 'py-3 px-6 text-base',
          hudText: 'text-base',
          controlSize: 'w-48 h-48',
          iconSize: 32,
          padding: 'p-3 sm:p-4'
        };
      case 'tablet':
        return {
          title: 'text-5xl md:text-6xl',
          subtitle: 'text-3xl md:text-4xl',
          button: 'py-4 px-8 text-lg',
          hudText: 'text-lg',
          controlSize: 'w-64 h-64',
          iconSize: 40,
          padding: 'p-4 md:p-6'
        };
      default: // desktop
        return {
          title: 'text-6xl lg:text-7xl',
          subtitle: 'text-4xl lg:text-5xl',
          button: 'py-4 px-8 text-xl',
          hudText: 'text-xl',
          controlSize: 'w-72 h-72',
          iconSize: 48,
          padding: 'p-4 lg:p-6'
        };
    }
  };

  const responsive = getResponsiveClasses();

  return (
    <div className="w-screen h-screen bg-black overflow-hidden select-none flex flex-col fixed inset-0">
      {/* Top HUD Bar - Outside Game Area */}
      {gameState === 'playing' && (
        <div className={`flex-shrink-0 bg-black/90 backdrop-blur-md border-b border-white/10 ${responsive.padding} pointer-events-auto`}>
          <div className="flex justify-between items-center max-w-6xl mx-auto">
            <div className="flex gap-2 sm:gap-4 items-center">
              <div className="bg-white/10 backdrop-blur-md rounded-lg px-3 py-2 sm:px-4 text-white">
                <div className="text-xs sm:text-sm opacity-80">Score</div>
                <div className={`${responsive.hudText} font-bold`}>{score.toLocaleString()}</div>
              </div>
              <div className="bg-white/10 backdrop-blur-md rounded-lg px-3 py-2 sm:px-4 text-white flex items-center gap-1 sm:gap-2">
                {Array.from({ length: lives }).map((_, i) => (
                   <Heart key={i} className="text-red-500 fill-current" size={deviceType === 'mobile' ? 20 : 24} />
                ))}
              </div>
            </div>
            <button
              onClick={pauseGame}
              className="bg-white/20 backdrop-blur-md hover:bg-white/30 rounded-lg p-2 sm:p-3 text-white transition-all duration-200 active:scale-95"
            >
              <Pause size={deviceType === 'mobile' ? 16 : 20} />
            </button>
          </div>
        </div>
      )}

      {/* Game Area */}
      <div className="flex-grow relative min-h-0">
        <canvas
          ref={canvasRef}
          className="absolute inset-0 w-full h-full"
          style={{ touchAction: 'none' }}
        />
        
        {/* Overlay Screens */}
        <div className="absolute inset-0">
          {/* Menu Screen */}
          {gameState === 'menu' && (
            <div className="absolute inset-0 bg-black/80 backdrop-blur-sm flex items-center justify-center pointer-events-auto">
              <div className="text-center text-white max-w-md mx-4">
                <h1 className={`${responsive.title} font-bold mb-2 bg-gradient-to-r from-blue-400 to-purple-600 bg-clip-text text-transparent`}>
                  STELLAR
                </h1>
                <h2 className={`${responsive.subtitle} font-bold mb-8 bg-gradient-to-r from-purple-600 to-pink-400 bg-clip-text text-transparent`}>
                  DEFENDER
                </h2>
                <div className="space-y-4">
                  <button
                    onClick={startGame}
                    className={`w-full bg-gradient-to-r from-blue-600 to-purple-600 hover:from-blue-700 hover:to-purple-700 text-white font-bold ${responsive.button} rounded-lg transition-all duration-200 transform hover:scale-105 active:scale-98`}
                  >
                    START GAME
                  </button>
                  <button
                    onClick={handleExit}
                    className={`w-full bg-gradient-to-r from-gray-600 to-gray-700 hover:from-gray-700 hover:to-gray-800 text-white font-bold ${responsive.button} rounded-lg transition-all duration-200 active:scale-98`}
                  >
                    <PowerOff className="inline mr-2" size={20} />
                    EXIT
                  </button>
                  <div className="bg-black/50 rounded-lg p-4">
                    <div className={`text-blue-400 ${deviceType === 'mobile' ? 'text-sm' : 'text-base'}`}>
                      High Score: <span className="font-bold">{highScore.toLocaleString()}</span>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          )}

          {/* Pause Screen */}
          {gameState === 'paused' && (
            <div className="absolute inset-0 bg-black/80 backdrop-blur-sm flex items-center justify-center pointer-events-auto">
              <div className="text-center text-white max-w-md mx-4">
                <h2 className={`${responsive.subtitle} font-bold mb-8`}>PAUSED</h2>
                <div className="space-y-4 w-64">
                    <button
                        onClick={resumeGame}
                        className={`w-full bg-gradient-to-r from-green-600 to-blue-600 hover:from-green-700 hover:to-blue-700 text-white font-bold ${responsive.button} rounded-lg transition-all duration-200 flex items-center justify-center gap-2 active:scale-98`}
                    >
                        <Play size={20} />
                        Resume Game
                    </button>
                    <button
                        onClick={restartGame}
                        className={`w-full bg-gradient-to-r from-orange-600 to-red-600 hover:from-orange-700 hover:to-red-700 text-white font-bold ${responsive.button} rounded-lg transition-all duration-200 flex items-center justify-center gap-2 active:scale-98`}
                    >
                        <RotateCcw size={20} />
                        Restart Game
                    </button>
                    <button
                        onClick={returnToMenu}
                        className={`w-full bg-gradient-to-r from-gray-600 to-gray-700 hover:from-gray-700 hover:to-gray-800 text-white font-bold ${responsive.button} rounded-lg transition-all duration-200 flex items-center justify-center gap-2 active:scale-98`}
                    >
                        <Home size={20} />
                        Main Menu
                    </button>
                </div>
              </div>
            </div>
          )}

          {/* Game Over Screen */}
          {gameState === 'gameOver' && (
            <div className="absolute inset-0 bg-black/90 backdrop-blur-sm flex items-center justify-center pointer-events-auto">
              <div className="text-center text-white max-w-md mx-4">
                <h2 className={`${responsive.subtitle} font-bold mb-4 text-red-400`}>GAME OVER</h2>
                <div className="bg-black/50 rounded-lg p-6 mb-6">
                  <div className={`${deviceType === 'mobile' ? 'text-xl' : 'text-2xl'} font-bold mb-2`}>Final Score</div>
                  <div className={`${responsive.subtitle} font-bold text-yellow-400 mb-4`}>{score.toLocaleString()}</div>
                  {score > highScore && (
                    <div className={`text-green-400 font-bold mb-2 ${deviceType === 'mobile' ? 'text-sm' : 'text-base'}`}>🎉 NEW HIGH SCORE! 🎉</div>
                  )}
                </div>
                <div className="space-y-4">
                  <button
                    onClick={startGame}
                    className={`w-full bg-gradient-to-r from-blue-600 to-purple-600 hover:from-blue-700 hover:to-purple-700 text-white font-bold ${responsive.button} rounded-lg transition-all duration-200 transform hover:scale-105 active:scale-98`}
                  >
                    PLAY AGAIN
                  </button>
                  <button
                    onClick={returnToMenu}
                    className={`w-full bg-gradient-to-r from-gray-600 to-gray-700 hover:from-gray-700 hover:to-gray-800 text-white font-bold ${responsive.button} rounded-lg transition-all duration-200 active:scale-98`}
                  >
                    MAIN MENU
                  </button>
                </div>
              </div>
            </div>
          )}
        </div>
      </div>
      
      {/* Bottom Controls Panel (Touch Devices Only) - Outside Game Area */}
      {isTouchDevice && gameState === 'playing' && (
        <div className={`flex-shrink-0 bg-black/90 backdrop-blur-md border-t border-white/10 ${responsive.padding} ${deviceType === 'mobile' ? 'pb-safe pb-8' : 'pb-12'} pointer-events-auto`}>
          <div className="max-w-md mx-auto">
            <div className="flex justify-center">
              <div className={`grid grid-cols-3 grid-rows-3 ${responsive.controlSize} gap-2 sm:gap-3`}>
                <div />
                <button
                    onTouchStart={() => gameRef.current?.setPlayerMovement('up', true)}
                    onTouchEnd={() => gameRef.current?.setPlayerMovement('up', false)}
                    className="bg-white/20 backdrop-blur-md rounded-xl text-white font-bold active:bg-white/40 transition-all duration-100 shadow-lg border border-white/20 active:scale-95 flex items-center justify-center hover:bg-white/30"
                >
                    <ArrowUp className="mx-auto" size={responsive.iconSize}/>
                </button>
                <div />
                <button
                    onTouchStart={() => gameRef.current?.setPlayerMovement('left', true)}
                    onTouchEnd={() => gameRef.current?.setPlayerMovement('left', false)}
                    className="bg-white/20 backdrop-blur-md rounded-xl text-white font-bold active:bg-white/40 transition-all duration-100 shadow-lg border border-white/20 active:scale-95 flex items-center justify-center hover:bg-white/30"
                >
                    <ArrowLeft className="mx-auto" size={responsive.iconSize}/>
                </button>
                <div className="bg-white/5 rounded-xl border border-white/10" />
                <button
                    onTouchStart={() => gameRef.current?.setPlayerMovement('right', true)}
                    onTouchEnd={() => gameRef.current?.setPlayerMovement('right', false)}
                    className="bg-white/20 backdrop-blur-md rounded-xl text-white font-bold active:bg-white/40 transition-all duration-100 shadow-lg border border-white/20 active:scale-95 flex items-center justify-center hover:bg-white/30"
                >
                    <ArrowRight className="mx-auto" size={responsive.iconSize}/>
                </button>
                <div />
                <button
                    onTouchStart={() => gameRef.current?.setPlayerMovement('down', true)}
                    onTouchEnd={() => gameRef.current?.setPlayerMovement('down', false)}
                    className="bg-white/20 backdrop-blur-md rounded-xl text-white font-bold active:bg-white/40 transition-all duration-100 shadow-lg border border-white/20 active:scale-95 flex items-center justify-center hover:bg-white/30"
                >
                    <ArrowDown className="mx-auto" size={responsive.iconSize}/>
                </button>
                <div />
              </div>
            </div>
          </div>
        </div>
      )}
    </div>
  );
}

// Game Engine Classes
class StellarDefenderGame {
  constructor(canvas, callbacks) {
    this.canvas = canvas;
    this.ctx = canvas.getContext('2d');
    this.callbacks = callbacks;
    this.isRunning = false;
    this.isPaused = false;
    this.deviceType = callbacks.deviceType || 'desktop'; // Get device type from callbacks
    
    this.player = new Player(0, 0);
    this.enemies = [];
    this.projectiles = [];
    this.particles = [];
    this.powerUps = [];
    this.stars = [];
    this.scoreTexts = [];
    
    this.wave = 1;
    this.score = 0;
    this.lives = 3;
    this.enemySpawnTimer = 0;
    this.waveTimer = 0;
    
    this.keys = {};
    this.mousePos = { x: 0, y: 0 };
    this.isTouching = false;
    
    this.playerMovement = { up: false, down: false, left: false, right: false };
    this.playSound = callbacks.playSound || (() => {});

    // Calculate safe play area boundaries based on device type
    this.getDeviceBoundaries();

    this.initializeBackground();
    this.setupEventListeners();
    
    this.lastTime = 0;
    this.gameLoop = this.gameLoop.bind(this);
  }

  getDeviceBoundaries() {
    const isTouchDevice = 'ontouchstart' in window || navigator.maxTouchPoints > 0;
    
    switch (this.deviceType) {
      case 'mobile':
        this.topHUDHeight = 60; // Reduced from 70 to move game area up
        this.bottomControlsHeight = isTouchDevice ? 220 : 0; // Reduced from 250
        break;
      case 'tablet':
        this.topHUDHeight = 90;
        this.bottomControlsHeight = isTouchDevice ? 320 : 0;
        break;
      default: // desktop
        this.topHUDHeight = 100;
        this.bottomControlsHeight = 0;
        break;
    }
  }

  setPlayerMovement(direction, isPressed) {
    if (this.playerMovement.hasOwnProperty(direction)) {
      this.playerMovement[direction] = isPressed;
    }
  }

  initializeBackground() {
    this.stars = [];
    // Adjust star count based on device performance
    const starCount = this.deviceType === 'mobile' ? 50 : this.deviceType === 'tablet' ? 100 : 200;
    for (let i = 0; i < starCount; i++) {
      this.stars.push({
        x: Math.random() * this.canvas.width,
        y: Math.random() * this.canvas.height,
        size: Math.random() * 2 + 0.5,
        speed: Math.random() * 1.5 + 0.2,
        opacity: Math.random() * 0.8 + 0.2
      });
    }
  }

  setupEventListeners() {
    const getTouchPos = (touch) => {
      const rect = this.canvas.getBoundingClientRect();
      return {
        x: (touch.clientX - rect.left) * (this.canvas.width / rect.width),
        y: (touch.clientY - rect.top) * (this.canvas.height / rect.height)
      };
    };

    this.canvas.addEventListener('touchstart', (e) => {
      this.isTouching = true;
      this.mousePos = getTouchPos(e.touches[0]);
    }, { passive: true });

    this.canvas.addEventListener('touchmove', (e) => {
      if (this.isTouching) {
        this.mousePos = getTouchPos(e.touches[0]);
      }
    }, { passive: true });

    this.canvas.addEventListener('touchend', (e) => {
      this.isTouching = false;
    }, { passive: true });

    window.addEventListener('mousedown', (e) => {
        if (e.target === this.canvas) {
            this.isTouching = true;
            const rect = this.canvas.getBoundingClientRect();
            this.mousePos = {
                x: (e.clientX - rect.left) * (this.canvas.width / rect.width),
                y: (e.clientY - rect.top) * (this.canvas.height / rect.height)
            };
        }
    });

    window.addEventListener('mousemove', (e) => {
        if (this.isTouching && e.target === this.canvas) {
            const rect = this.canvas.getBoundingClientRect();
            this.mousePos = {
                x: (e.clientX - rect.left) * (this.canvas.width / rect.width),
                y: (e.clientY - rect.top) * (this.canvas.height / rect.height)
            };
        }
    });

    window.addEventListener('mouseup', () => { this.isTouching = false; });
    window.addEventListener('keydown', (e) => { this.keys[e.key.toLowerCase()] = true; });
    window.addEventListener('keyup', (e) => { this.keys[e.key.toLowerCase()] = false; });
  }

  resize() {
    const container = this.canvas.parentElement;
    if (!container) return;
    const dpr = window.devicePixelRatio || 1;
    this.canvas.width = container.clientWidth * dpr;
    this.canvas.height = container.clientHeight * dpr;
    this.ctx.scale(dpr, dpr);
    this.canvas.style.width = `${container.clientWidth}px`;
    this.canvas.style.height = `${container.clientHeight}px`;
    this.getDeviceBoundaries(); // Re-calculate boundaries on resize
    this.initializeBackground(); // Re-initialize background based on new dimensions/device type
  }

  start() {
    this.isRunning = true;
    this.isPaused = false;
    this.score = 0;
    this.wave = 1;
    this.lives = 3;
    this.enemies = [];
    this.projectiles = [];
    this.particles = [];
    this.powerUps = [];
    this.scoreTexts = [];
    
    // Spawn player in the initial safe area
    const canvasWidth = this.canvas.width / window.devicePixelRatio;
    // Recalculate play area bottom just in case
    const canvasHeight = this.canvas.height / window.devicePixelRatio;
    const playAreaBottom = canvasHeight - this.bottomControlsHeight;
    this.player.spawn(canvasWidth / 2, playAreaBottom - 100);

    this.callbacks.onLivesUpdate(this.lives);
    this.lastTime = performance.now();
    requestAnimationFrame(this.gameLoop);
  }

  pause() { 
    this.isPaused = true; 
  }

  resume() {
    this.isPaused = false;
    this.lastTime = performance.now();
    requestAnimationFrame(this.gameLoop);
  }

  stop() { 
    this.isRunning = false;
    this.isPaused = true;
  }
  destroy() { this.stop(); }

  addScoreText(x, y, points) {
    this.scoreTexts.push({
      x: x,
      y: y,
      text: `+${points}`,
      life: 1.0,
      decay: 0.02
    });
  }

  gameLoop(currentTime) {
    if (!this.isRunning || this.isPaused) return;

    let deltaTime = currentTime - this.lastTime;
    this.lastTime = currentTime;
    
    // Cap deltaTime for stability, especially on mobile
    if (isNaN(deltaTime) || deltaTime > 50) deltaTime = 16.67;

    this.update(deltaTime);
    this.render();

    requestAnimationFrame(this.gameLoop);
  }

  update(deltaTime) {
    const canvasWidth = this.canvas.width / window.devicePixelRatio;
    const canvasHeight = this.canvas.height / window.devicePixelRatio;

    // Calculate safe play area
    const playAreaTop = this.topHUDHeight;
    const playAreaBottom = canvasHeight - this.bottomControlsHeight;

    // Handle player movement
    let dx = 0, dy = 0;
    if (this.keys['arrowleft'] || this.keys['a'] || this.playerMovement.left) dx = -1;
    if (this.keys['arrowright'] || this.keys['d'] || this.playerMovement.right) dx = 1;
    if (this.keys['arrowup'] || this.keys['w'] || this.playerMovement.up) dy = -1;
    if (this.keys['arrowdown'] || this.keys['s'] || this.playerMovement.down) dy = 1;
    
    if (this.isTouching) {
        // Constrain touch target to safe play area
        const constrainedMousePos = {
            x: Math.max(this.player.radius, Math.min(this.mousePos.x, canvasWidth - this.player.radius)),
            y: Math.max(playAreaTop + this.player.radius, Math.min(this.mousePos.y, playAreaBottom - this.player.radius))
        };
        this.player.moveTowards(constrainedMousePos.x, constrainedMousePos.y, deltaTime);
    } else if (dx !== 0 || dy !== 0) {
        this.player.move(dx, dy, deltaTime);
    }
    
    this.player.update(deltaTime, canvasWidth, playAreaTop, playAreaBottom);

    if (this.player.canFire()) {
      this.projectiles.push(...this.player.fire());
      this.playSound('shoot');
    }

    this.projectiles = this.projectiles.filter(p => p.update(deltaTime) && p.y > -50 && p.y < canvasHeight + 50);

    this.enemies.forEach(e => {
        e.update(deltaTime);
        if (e.canFire() && Math.random() < 0.02) this.projectiles.push(...e.fire());
    });
    this.enemies = this.enemies.filter(e => e.y < canvasHeight + 50 && e.health > 0);

    this.particles = this.particles.filter(p => p.update(deltaTime) && p.life > 0);
    this.powerUps = this.powerUps.filter(p => p.update(deltaTime) && p.y < canvasHeight + 50);

    this.scoreTexts.forEach(st => {
      st.life -= st.decay;
      st.y -= 30 * deltaTime / 1000;
    });
    this.scoreTexts = this.scoreTexts.filter(st => st.life > 0);

    this.stars.forEach(s => {
        s.y += s.speed;
        if (s.y > canvasHeight) { s.y = -5; s.x = Math.random() * canvasWidth; }
    });

    this.checkCollisions();
    this.spawnEnemies(deltaTime);
    this.updateWave(deltaTime);

    this.callbacks.onScoreUpdate(this.score);
  }

  playerDied() {
      this.lives--;
      this.callbacks.onLivesUpdate(this.lives);
      this.createExplosion(this.player.x, this.player.y, 'large');
      
      if (this.lives > 0) {
          const canvasWidth = this.canvas.width / window.devicePixelRatio;
          const canvasHeight = this.canvas.height / window.devicePixelRatio;
          const playAreaBottom = canvasHeight - this.bottomControlsHeight;
          this.player.spawn(canvasWidth / 2, playAreaBottom - 100);
      } else {
          this.gameOver();
      }
  }

  checkCollisions() {
    for (let i = this.projectiles.length - 1; i >= 0; i--) {
      const p = this.projectiles[i];
      if (!p) continue;
      if (p.isPlayerProjectile) {
        for (let j = this.enemies.length - 1; j >= 0; j--) {
          const e = this.enemies[j];
          if (!e) continue;
          if (this.checkCollision(p, e)) {
            e.health -= p.damage;
            this.createExplosion(p.x, p.y, 'small');
            if(i < this.projectiles.length) this.projectiles.splice(i, 1);
            if (e.health <= 0) {
              this.createExplosion(e.x, e.y, 'large');
              this.score += 3;
              this.addScoreText(e.x, e.y, 3);
              if (Math.random() < 0.15) this.powerUps.push(new PowerUp(e.x, e.y));
              if(j < this.enemies.length) this.enemies.splice(j, 1);
            }
            break;
          }
        }
      } else { // Enemy projectile
        if (this.checkCollision(p, this.player)) {
          if (this.player.takeDamage(p.damage)) this.playerDied();
          this.createExplosion(p.x, p.y, 'small');
          if(i < this.projectiles.length) this.projectiles.splice(i, 1);
        }
      }
    }

    for (let i = this.enemies.length - 1; i >= 0; i--) {
      const e = this.enemies[i];
      if (!e) continue;
      if (this.checkCollision(this.player, e)) {
        if (this.player.takeDamage(e.damage)) this.playerDied();
        this.createExplosion(e.x, e.y, 'large');
        if(i < this.enemies.length) this.enemies.splice(i, 1);
      }
    }

    for (let i = this.powerUps.length - 1; i >= 0; i--) {
      const pu = this.powerUps[i];
      if (!pu) continue;
      if (this.checkCollision(this.player, pu)) {
        this.player.applyPowerUp(pu.type);
        if(i < this.powerUps.length) this.powerUps.splice(i, 1);
      }
    }
  }

  checkCollision(obj1, obj2) {
    const dx = obj1.x - obj2.x;
    const dy = obj1.y - obj2.y;
    return (dx * dx + dy * dy) < (obj1.radius + obj2.radius) * (obj1.radius + obj2.radius);
  }

  createExplosion(x, y, size) {
    // Adjust particle count based on device performance
    const pCount = size === 'large' ? 
      (this.deviceType === 'mobile' ? 10 : this.deviceType === 'tablet' ? 15 : 25) : 
      (this.deviceType === 'mobile' ? 3 : this.deviceType === 'tablet' ? 5 : 10);
    
    const colors = ['#ff6b35', '#f7931e', '#ffd700', '#ff4757'];
    for (let i = 0; i < pCount; i++) {
      this.particles.push(new Particle(x, y, colors[Math.floor(Math.random() * colors.length)]));
    }
  }

  spawnEnemies(deltaTime) {
    const canvasWidth = this.canvas.width / window.devicePixelRatio;
    this.enemySpawnTimer += deltaTime;
    const spawnRate = Math.max(1200 - this.wave * 50, 400);
    if (this.enemySpawnTimer > spawnRate) {
      this.enemySpawnTimer = 0;
      const r = Math.random();
      const randomX = Math.random() * canvasWidth;
      if (this.wave > 3 && r > 0.95) this.enemies.push(new Boss(randomX, -100));
      else if (r > 0.5) this.enemies.push(new AlienShip(randomX, -50));
      else this.enemies.push(new Meteor(randomX, -50));
    }
  }

  updateWave(deltaTime) {
    this.waveTimer += deltaTime;
    if (this.waveTimer > 30000) { this.wave++; this.waveTimer = 0; }
  }

  gameOver() {
    this.isRunning = false;
    this.callbacks.onGameOver();
  }

  render() {
    const canvasWidth = this.canvas.width / window.devicePixelRatio;
    const canvasHeight = this.canvas.height / window.devicePixelRatio;
    
    this.ctx.fillStyle = '#000014';
    this.ctx.fillRect(0, 0, canvasWidth, canvasHeight);

    this.stars.forEach(star => {
        this.ctx.fillStyle = `rgba(255, 255, 255, ${star.opacity})`;
        this.ctx.beginPath();
        this.ctx.arc(star.x, star.y, star.size, 0, Math.PI * 2);
        this.ctx.fill();
    });

    this.particles.forEach(p => p.render(this.ctx));
    this.powerUps.forEach(p => p.render(this.ctx));
    this.enemies.forEach(e => e.render(this.ctx));
    this.projectiles.forEach(p => p.render(this.ctx));
    
    if (this.player.health > 0) {
      this.player.render(this.ctx);
    }
    
    this.ctx.save();
    this.ctx.globalAlpha = 1;
    this.scoreTexts.forEach(st => {
      this.ctx.globalAlpha = st.life;
      this.ctx.fillStyle = `rgb(255, 255, 0)`;
      // Adjust score text font size based on device type
      this.ctx.font = `bold ${this.deviceType === 'mobile' ? '12px' : '16px'} Arial`;
      this.ctx.textAlign = 'center';
      this.ctx.fillText(st.text, st.x, st.y);
    });
    this.ctx.restore();

    // Wave indicator
    this.ctx.fillStyle = 'rgba(255, 255, 255, 0.8)';
    // Adjust wave indicator font size and position based on device type
    this.ctx.font = `${this.deviceType === 'mobile' ? '16px' : '20px'} Arial`;
    this.ctx.textAlign = 'center';
    this.ctx.fillText(`Wave ${this.wave}`, canvasWidth / 2, this.deviceType === 'mobile' ? 40 : 50);
  }
}

class Player {
  constructor(x, y) {
    this.radius = 25;
    this.speed = 350;
    this.maxHealth = 100;
    this.fireRate = 200;
    this.damage = 25;
    this.spawn(x,y);
    this.powerUps = {};
  }

  spawn(x, y) {
    this.x = x;
    this.y = y;
    this.health = this.maxHealth;
    this.lastFire = 0;
    this.isInvincible = true;
    this.invincibleTimer = 3000;
  }

  update(deltaTime, canvasWidth, playAreaTop, playAreaBottom) {
    if (this.isInvincible) {
      this.invincibleTimer -= deltaTime;
      if (this.invincibleTimer <= 0) {
        this.isInvincible = false;
      }
    }
    Object.keys(this.powerUps).forEach(key => {
      this.powerUps[key] -= deltaTime;
      if (this.powerUps[key] <= 0) delete this.powerUps[key];
    });

    // Enforce strict boundaries within the safe play area
    this.x = Math.max(this.radius, Math.min(this.x, canvasWidth - this.radius));
    this.y = Math.max(playAreaTop + this.radius, Math.min(this.y, playAreaBottom - this.radius));
  }

  move(dx, dy, deltaTime) {
    const currentSpeed = this.speed * (this.powerUps.speedBoost ? 1.5 : 1);
    const moveSpeed = currentSpeed * deltaTime / 1000;
    const mag = Math.sqrt(dx*dx + dy*dy) || 1;
    this.x += (dx / mag) * moveSpeed;
    this.y += (dy / mag) * moveSpeed;
  }

  moveTowards(targetX, targetY, deltaTime) {
    const dx = targetX - this.x;
    const dy = targetY - this.y;
    const dist = Math.sqrt(dx*dx + dy*dy);
    if (dist > 5) {
      const currentSpeed = this.speed * (this.powerUps.speedBoost ? 1.5 : 1);
      const moveSpeed = currentSpeed * deltaTime / 1000;
      this.x += (dx / dist) * moveSpeed;
      this.y += (dy / dist) * moveSpeed;
    }
  }

  canFire() { return Date.now() - this.lastFire > this.fireRate; }

  fire() {
    this.lastFire = Date.now();
    const projectiles = [];
    const damage = this.damage * (this.powerUps.damageBoost ? 1.5 : 1);
    
    if (this.powerUps.multiShot) {
      projectiles.push(new Projectile(this.x - 10, this.y - 20, 0, -500, damage, true), new Projectile(this.x, this.y - 20, 0, -500, damage, true), new Projectile(this.x + 10, this.y - 20, 0, -500, damage, true));
    } else if (this.powerUps.spreadShot) {
      projectiles.push(new Projectile(this.x, this.y - 20, -100, -500, damage, true), new Projectile(this.x, this.y - 20, 0, -500, damage, true), new Projectile(this.x, this.y - 20, 100, -500, damage, true));
    } else {
      projectiles.push(new Projectile(this.x, this.y - 20, 0, -500, damage, true));
    }
    return projectiles;
  }

  takeDamage(damage) {
    if (this.isInvincible) return false;
    if (this.powerUps.shield) {
        delete this.powerUps.shield;
        return false;
    }
    this.health -= damage;
    return this.health <= 0;
  }

  applyPowerUp(type) { 
    this.powerUps[type] = 10000;
    if (type === 'shield') {
      this.powerUps[type] = 15000;
    }
  }

  render(ctx) {
    if (this.isInvincible && Math.floor(Date.now() / 100) % 2 === 0) return;
    
    // Shield effect
    if (this.powerUps.shield) {
      const time = Date.now() / 1000;
      const shieldOpacity = 0.5 + Math.sin(time * 5) * 0.3;
      ctx.strokeStyle = `rgba(0, 150, 255, ${shieldOpacity})`;
      ctx.fillStyle = `rgba(0, 150, 255, ${shieldOpacity * 0.2})`;
      ctx.lineWidth = 3;
      ctx.beginPath();
      ctx.arc(this.x, this.y, this.radius + 15, 0, Math.PI * 2);
      ctx.stroke();
      ctx.fill();
    }

    // Realistic rocket body
    ctx.save();
    
    // Main body (metallic silver)
    const gradient = ctx.createLinearGradient(this.x - this.radius, this.y, this.x + this.radius, this.y);
    gradient.addColorStop(0, '#c0c0c0');
    gradient.addColorStop(0.5, '#ffffff');
    gradient.addColorStop(1, '#808080');
    
    ctx.fillStyle = gradient;
    ctx.beginPath();
    ctx.ellipse(this.x, this.y, this.radius * 0.6, this.radius, 0, 0, Math.PI * 2);
    ctx.fill();
    
    // Nose cone (darker metal)
    ctx.fillStyle = '#606060';
    ctx.beginPath();
    ctx.moveTo(this.x, this.y - this.radius);
    ctx.lineTo(this.x - this.radius * 0.4, this.y - this.radius * 0.4);
    ctx.lineTo(this.x + this.radius * 0.4, this.y - this.radius * 0.4);
    ctx.closePath();
    ctx.fill();
    
    // Wings/fins
    ctx.fillStyle = '#4a4a4a';
    ctx.beginPath();
    ctx.moveTo(this.x - this.radius * 0.6, this.y + this.radius * 0.3);
    ctx.lineTo(this.x - this.radius * 1.2, this.y + this.radius * 0.8);
    ctx.lineTo(this.x - this.radius * 0.3, this.y + this.radius * 0.6);
    ctx.closePath();
    ctx.fill();
    
    ctx.beginPath();
    ctx.moveTo(this.x + this.radius * 0.6, this.y + this.radius * 0.3);
    ctx.lineTo(this.x + this.radius * 1.2, this.y + this.radius * 0.8);
    ctx.lineTo(this.x + this.radius * 0.3, this.y + this.radius * 0.6);
    ctx.closePath();
    ctx.fill();
    
    // Engine flames
    const flameHeight = this.radius * 1.2 + Math.random() * 5;
    const flameWidth = this.radius * 0.8;
    
    // Outer flame (orange)
    ctx.fillStyle = '#ff6b35';
    ctx.beginPath();
    ctx.moveTo(this.x - flameWidth/2, this.y + this.radius * 0.8);
    ctx.lineTo(this.x + flameWidth/2, this.y + this.radius * 0.8);
    ctx.lineTo(this.x, this.y + this.radius * 0.8 + flameHeight);
    ctx.closePath();
    ctx.fill();
    
    // Inner flame (blue-white)
    ctx.fillStyle = '#00bfff';
    ctx.beginPath();
    ctx.moveTo(this.x - flameWidth/4, this.y + this.radius * 0.8);
    ctx.lineTo(this.x + flameWidth/4, this.y + this.radius * 0.8);
    ctx.lineTo(this.x, this.y + this.radius * 0.8 + flameHeight * 0.7);
    ctx.closePath();
    ctx.fill();
    
    // Window/cockpit
    ctx.fillStyle = 'rgba(100, 150, 255, 0.8)';
    ctx.beginPath();
    ctx.arc(this.x, this.y - this.radius * 0.2, this.radius * 0.3, 0, Math.PI * 2);
    ctx.fill();
    
    ctx.restore();

    // Health bar
    const barW = 40, barH = 4, barX = this.x - barW / 2, barY = this.y - this.radius - 20;
    ctx.fillStyle = 'rgba(255, 0, 0, 0.7)';
    ctx.fillRect(barX, barY, barW, barH);
    ctx.fillStyle = 'rgba(0, 255, 0, 0.7)';
    ctx.fillRect(barX, barY, barW * (this.health / this.maxHealth), barH);
  }
}

class Projectile {
  constructor(x, y, vx, vy, damage, isPlayerProjectile = false) {
    this.x = x; this.y = y; this.vx = vx; this.vy = vy;
    this.damage = damage; this.isPlayerProjectile = isPlayerProjectile;
    this.radius = 4;
  }
  update(deltaTime) {
    const factor = deltaTime / 1000;
    this.x += this.vx * factor;
    this.y += this.vy * factor;
    return true;
  }
  render(ctx) {
    ctx.fillStyle = this.isPlayerProjectile ? '#00ff88' : '#ff4757';
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
    ctx.fill();
    
    // Glow effect
    ctx.shadowBlur = 10;
    ctx.shadowColor = this.isPlayerProjectile ? '#00ff88' : '#ff4757';
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
    ctx.fill();
    ctx.shadowBlur = 0;
  }
}

class Enemy {
  constructor(x, y, health, points) {
    this.x = x; this.y = y; this.health = health; this.maxHealth = health;
    this.points = points; this.damage = 25; this.radius = 15;
    this.speed = 150; this.fireRate = 1000; this.lastFire = Date.now();
  }
  update(deltaTime) { 
    this.y += this.speed * deltaTime / 1000; 
  }
  canFire() { return Date.now() - this.lastFire > this.fireRate; }
  fire() {
    this.lastFire = Date.now();
    return [new Projectile(this.x, this.y + this.radius, 0, 300, this.damage, false)];
  }
  render(ctx) {
    if (this.health < this.maxHealth) {
      const barW = 30, barH = 3, barX = this.x - barW / 2, barY = this.y - this.radius - 10;
      ctx.fillStyle = 'rgba(255, 0, 0, 0.7)'; ctx.fillRect(barX, barY, barW, barH);
      ctx.fillStyle = 'rgba(0, 255, 0, 0.7)'; ctx.fillRect(barX, barY, barW * (this.health / this.maxHealth), barH);
    }
  }
}

class Meteor extends Enemy {
  constructor(x, y) {
    super(x, y, 50, 50);
    this.radius = 20 + Math.random() * 10;
    this.speed = 100 + Math.random() * 100;
    this.rotation = 0;
    this.rotationSpeed = Math.random() * 2 - 1;
  }
  canFire() { return false; }
  update(deltaTime) {
    super.update(deltaTime);
    this.rotation += this.rotationSpeed * deltaTime / 1000;
  }
  render(ctx) {
    super.render(ctx);
    ctx.save();
    ctx.translate(this.x, this.y);
    ctx.rotate(this.rotation);
    ctx.fillStyle = '#8B4513'; ctx.beginPath(); ctx.arc(0, 0, this.radius, 0, Math.PI * 2); ctx.fill();
    ctx.fillStyle = '#A0522D'; ctx.beginPath(); ctx.arc(-5, -5, this.radius * 0.4, 0, Math.PI * 2); ctx.fill();
    ctx.beginPath(); ctx.arc(7, 3, this.radius * 0.2, 0, Math.PI * 2); ctx.fill();
    ctx.restore();
  }
}

class AlienShip extends Enemy {
  constructor(x, y) {
    super(x, y, 75, 100);
    this.radius = 18;
    this.speed = 120;
    this.fireRate = 1200;
    this.zigzag = Math.random() * Math.PI * 2;
  }
  update(deltaTime) {
    super.update(deltaTime);
    this.zigzag += deltaTime / 1000 * 2;
    this.x += Math.sin(this.zigzag) * 60 * deltaTime / 1000;
  }
  render(ctx) {
    super.render(ctx);
    ctx.save();
    
    // Main saucer body - Realistic metallic design
    const gradient = ctx.createRadialGradient(this.x, this.y, this.radius * 0.2, this.x, this.y, this.radius);
    gradient.addColorStop(0, '#a8a8a8');
    gradient.addColorStop(0.3, '#7f8c8d');
    gradient.addColorStop(0.7, '#5a6c75');
    gradient.addColorStop(1, '#34495e');
    ctx.fillStyle = gradient;
    ctx.beginPath();
    ctx.ellipse(this.x, this.y, this.radius, this.radius * 0.7, 0, 0, Math.PI * 2);
    ctx.fill();
    
    // Metallic rim
    ctx.strokeStyle = '#95a5a6';
    ctx.lineWidth = 2;
    ctx.beginPath();
    ctx.ellipse(this.x, this.y, this.radius, this.radius * 0.7, 0, 0, Math.PI * 2);
    ctx.stroke();
    
    // Cockpit dome
    const cockpitGradient = ctx.createRadialGradient(this.x, this.y - 2, 1, this.x, this.y, this.radius * 0.6);
    cockpitGradient.addColorStop(0, '#85c1e9');
    cockpitGradient.addColorStop(0.5, '#5dade2');
    cockpitGradient.addColorStop(1, '#2e86ab');
    ctx.fillStyle = cockpitGradient;
    ctx.beginPath();
    ctx.arc(this.x, this.y - 2, this.radius * 0.6, 0, Math.PI, true);
    ctx.fill();
    
    // Engine ports
    ctx.fillStyle = '#e74c3c';
    for (let i = 0; i < 4; i++) {
      const angle = (Math.PI / 2) * i;
      const portX = this.x + Math.cos(angle) * this.radius * 0.8;
      const portY = this.y + Math.sin(angle) * this.radius * 0.6;
      ctx.beginPath();
      ctx.arc(portX, portY, 3, 0, Math.PI * 2);
      ctx.fill();
    }

    ctx.restore();
  }
}

class Boss extends Enemy {
  constructor(x, y) {
    super(x, y, 500, 1000);
    this.radius = 40; this.speed = 80; this.fireRate = 400;
    this.phase = 0; this.phaseTimer = 0;
  }
  update(deltaTime) {
    super.update(deltaTime);
    this.phaseTimer += deltaTime;
    if (this.phaseTimer > 5000) { this.phase = (this.phase + 1) % 3; this.phaseTimer = 0; }
    if (this.phase === 0) this.x += Math.sin(Date.now() / 1000) * 100 * deltaTime / 1000;
    else if (this.phase === 1) this.x += Math.cos(Date.now() / 1000) * 80 * deltaTime / 1000;
    else this.speed = 150;
  }
  fire() {
    this.lastFire = Date.now();
    const projectiles = [];
    if (this.phase === 2) {
        for (let i = 0; i < 3; i++) {
            projectiles.push(new Projectile(this.x, this.y + this.radius, (Math.random() - 0.5) * 400, 300, this.damage, false));
        }
    } else {
        for (let i = 0; i < 5; i++) {
          const angle = (Math.PI / 4) * (i - 2);
          const vx = Math.sin(angle) * 200, vy = Math.cos(angle) * 200;
          projectiles.push(new Projectile(this.x, this.y + this.radius, vx, vy, this.damage, false));
        }
    }
    return projectiles;
  }
  render(ctx) {
    super.render(ctx);
    ctx.save();
    
    // Main hull - Advanced battleship design
    const hullGradient = ctx.createLinearGradient(this.x - this.radius, this.y, this.x + this.radius, this.y);
    hullGradient.addColorStop(0, '#6c7b7f');
    hullGradient.addColorStop(0.3, '#95a5a6');
    hullGradient.addColorStop(0.5, '#bdc3c7');
    hullGradient.addColorStop(0.7, '#95a5a6');
    hullGradient.addColorStop(1, '#5d6d70');
    ctx.fillStyle = hullGradient;
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
    ctx.fill();
    
    // Armored plating
    ctx.strokeStyle = '#7f8c8d';
    ctx.lineWidth = 3;
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
    ctx.stroke();
    
    // Central weapon system
    const weaponGradient = ctx.createRadialGradient(this.x, this.y, 2, this.x, this.y, this.radius * 0.5);
    weaponGradient.addColorStop(0, '#ff6b81');
    weaponGradient.addColorStop(0.5, '#e55572');
    weaponGradient.addColorStop(1, '#c0392b');
    ctx.fillStyle = weaponGradient;
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.radius * 0.5, 0, Math.PI * 2);
    ctx.fill();
    
    // Side weapon pods
    const podRadius = this.radius * 0.3;
    for (let i = -1; i <= 1; i += 2) {
      const podX = this.x + (this.radius * 0.9) * i;
      const podY = this.y + this.radius * 0.2;
      
      // Pod body
      ctx.fillStyle = '#5a6c75';
      ctx.beginPath();
      ctx.arc(podX, podY, podRadius, 0, Math.PI * 2);
      ctx.fill();
      
      // Pod weapon
      ctx.fillStyle = '#e74c3c';
      ctx.beginPath();
      ctx.arc(podX, podY, podRadius * 0.4, 0, Math.PI * 2);
      ctx.fill();
    }
    
    ctx.restore();
  }
}

class PowerUp {
  constructor(x, y) {
    this.x = x; this.y = y; this.radius = 12; this.speed = 100;
    this.type = ['multiShot', 'spreadShot', 'shield', 'speedBoost', 'damageBoost'][Math.floor(Math.random() * 5)];
    this.pulse = 0;
  }
  update(deltaTime) { this.y += this.speed * deltaTime / 1000; this.pulse += deltaTime / 1000 * 5; return true; }
  render(ctx) {
    const pulseSize = Math.sin(this.pulse) * 3;
    ctx.fillStyle = this.getColor(); ctx.beginPath(); ctx.arc(this.x, this.y, this.radius + pulseSize, 0, Math.PI * 2); ctx.fill();
    ctx.fillStyle = 'white'; ctx.font = 'bold 12px Arial'; ctx.textAlign = 'center';
    ctx.fillText(this.getSymbol(), this.x, this.y + 4);
  }
  getColor() {
    switch (this.type) {
      case 'multiShot': return '#00ff88'; case 'spreadShot': return '#ff9f43';
      case 'shield': return '#0abde3'; case 'speedBoost': return '#ee5a6f';
      case 'damageBoost': return '#e056fd';
      default: return '#ffffff';
    }
  }
  getSymbol() {
    switch (this.type) {
      case 'multiShot': return '|||'; case 'spreadShot': return '><';
      case 'shield': return '◊'; case 'speedBoost': return '»';
      case 'damageBoost': return '⚡';
      default: return '?';
    }
  }
}

class Particle {
  constructor(x, y, color) {
    this.x = x; this.y = y; 
    const angle = Math.random() * Math.PI * 2;
    const speed = Math.random() * 150 + 50;
    this.vx = Math.cos(angle) * speed;
    this.vy = Math.sin(angle) * speed;
    this.color = color;
    this.size = Math.random() * 4 + 2; this.life = 1;
    this.decay = Math.random() * 0.02 + 0.01;
  }
  update(deltaTime) {
    const factor = deltaTime / 1000;
    this.x += this.vx * factor; this.y += this.vy * factor;
    this.life -= this.decay; this.size *= 0.98;
    return this.life > 0;
  }
  render(ctx) {
    ctx.globalAlpha = this.life; ctx.fillStyle = this.color;
    ctx.beginPath(); ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2); ctx.fill();
    ctx.globalAlpha = 1;
  }
}
