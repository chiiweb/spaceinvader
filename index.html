import React, { useState, useEffect, useRef } from 'react';
import { Volume2, VolumeX, Heart } from 'lucide-react';

const SpaceInvadersGame = () => {
  const canvasRef = useRef(null);
  const [gameState, setGameState] = useState('menu');
  const [username, setUsername] = useState('');
  const [selectedChar, setSelectedChar] = useState(0);
  const [score, setScore] = useState(0);
  const [lives, setLives] = useState(3);
  const [leaderboard, setLeaderboard] = useState([]);
  const [muted, setMuted] = useState(false);
  const gameLoopRef = useRef(null);
  const gameDataRef = useRef(null);

  const characters = [
    { colors: ['#7B2CBF', '#FFFFFF', '#C77DFF'], name: 'Purple' },
    { colors: ['#FF006E', '#FFFFFF', '#FB5607'], name: 'Red' },
    { colors: ['#06FFA5', '#FFFFFF', '#08B2E3'], name: 'Cyan' }
  ];

  const audioRefs = useRef({
    menu: null,
    game: null,
    gameover: null
  });

  useEffect(() => {
    loadLeaderboard();
  }, []);

  const loadLeaderboard = async () => {
    try {
      const result = await window.storage.list('score:', true);
      if (result && result.keys) {
        const scores = await Promise.all(
          result.keys.map(async (key) => {
            try {
              const data = await window.storage.get(key, true);
              return data ? JSON.parse(data.value) : null;
            } catch {
              return null;
            }
          })
        );
        const validScores = scores.filter(s => s).sort((a, b) => b.score - a.score).slice(0, 10);
        setLeaderboard(validScores);
      }
    } catch (e) {
      setLeaderboard([]);
    }
  };

  const saveScore = async (name, finalScore) => {
    try {
      const timestamp = Date.now();
      const scoreData = { username: name, score: finalScore, timestamp };
      await window.storage.set(`score:${timestamp}`, JSON.stringify(scoreData), true);
      await loadLeaderboard();
    } catch (e) {
      console.error('Failed to save score:', e);
    }
  };

  const playAudio = (type) => {
    if (muted) return;
    Object.values(audioRefs.current).forEach(audio => {
      if (audio) {
        audio.pause();
        audio.currentTime = 0;
      }
    });
    if (audioRefs.current[type]) {
      audioRefs.current[type].loop = type !== 'gameover';
      audioRefs.current[type].play().catch(() => {});
    }
  };

  const initGame = () => {
    const canvas = canvasRef.current;
    const ctx = canvas.getContext('2d');
    const colors = characters[selectedChar].colors;

    const game = {
      player: { x: canvas.width / 2 - 15, y: canvas.height - 60, width: 30, height: 30, speed: 5 },
      bullets: [],
      enemies: [],
      enemyBullets: [],
      enemySpeed: 1,
      enemyDirection: 1,
      score: 0,
      lives: 3,
      keys: {},
      lastShot: 0,
      lastEnemyShot: 0,
      invincible: false,
      invincibleTimer: 0
    };

    for (let row = 0; row < 4; row++) {
      for (let col = 0; col < 8; col++) {
        game.enemies.push({
          x: col * 50 + 50,
          y: row * 40 + 50,
          width: 30,
          height: 30,
          alive: true
        });
      }
    }

    const drawPlayer = () => {
      if (game.invincible && Math.floor(Date.now() / 100) % 2 === 0) {
        ctx.globalAlpha = 0.3;
      }
      ctx.fillStyle = colors[0];
      ctx.fillRect(game.player.x, game.player.y, game.player.width, game.player.height);
      ctx.fillStyle = colors[1];
      ctx.fillRect(game.player.x + 7, game.player.y + 8, 6, 6);
      ctx.fillRect(game.player.x + 17, game.player.y + 8, 6, 6);
      ctx.fillRect(game.player.x + 10, game.player.y + 20, 10, 3);
      ctx.globalAlpha = 1;
    };

    const drawEnemy = (enemy) => {
      ctx.fillStyle = colors[2];
      ctx.fillRect(enemy.x, enemy.y, enemy.width, enemy.height);
      ctx.fillStyle = colors[1];
      ctx.fillRect(enemy.x + 7, enemy.y + 10, 5, 5);
      ctx.fillRect(enemy.x + 18, enemy.y + 10, 5, 5);
      ctx.fillRect(enemy.x + 5, enemy.y + 5, 3, 3);
      ctx.fillRect(enemy.x + 22, enemy.y + 5, 3, 3);
    };

    const loseLife = () => {
      game.lives--;
      setLives(game.lives);
      game.invincible = true;
      game.invincibleTimer = Date.now();
      game.player.x = canvas.width / 2 - 15;
      game.enemyBullets = [];
      
      if (game.lives <= 0) {
        endGame();
      }
    };

    const update = () => {
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      if (game.invincible && Date.now() - game.invincibleTimer > 2000) {
        game.invincible = false;
      }

      if (game.keys['ArrowLeft'] && game.player.x > 0) {
        game.player.x -= game.player.speed;
      }
      if (game.keys['ArrowRight'] && game.player.x < canvas.width - game.player.width) {
        game.player.x += game.player.speed;
      }
      if (game.keys[' '] && Date.now() - game.lastShot > 300) {
        game.bullets.push({ x: game.player.x + 12, y: game.player.y, width: 4, height: 10 });
        game.lastShot = Date.now();
      }

      game.bullets.forEach((bullet, i) => {
        bullet.y -= 7;
        if (bullet.y < 0) {
          game.bullets.splice(i, 1);
        } else {
          ctx.fillStyle = colors[1];
          ctx.fillRect(bullet.x, bullet.y, bullet.width, bullet.height);
        }
      });

      let moveDown = false;
      game.enemies.forEach(enemy => {
        if (enemy.alive) {
          enemy.x += game.enemySpeed * game.enemyDirection;
          if (enemy.x <= 0 || enemy.x >= canvas.width - enemy.width) {
            moveDown = true;
          }
        }
      });

      if (moveDown) {
        game.enemyDirection *= -1;
        game.enemies.forEach(enemy => {
          if (enemy.alive) enemy.y += 20;
        });
      }

      game.enemies.forEach((enemy, i) => {
        if (enemy.alive) {
          drawEnemy(enemy);
          
          game.bullets.forEach((bullet, j) => {
            if (bullet.x < enemy.x + enemy.width &&
                bullet.x + bullet.width > enemy.x &&
                bullet.y < enemy.y + enemy.height &&
                bullet.y + bullet.height > enemy.y) {
              enemy.alive = false;
              game.bullets.splice(j, 1);
              game.score += 10;
              setScore(game.score);
            }
          });

          if (enemy.y + enemy.height >= game.player.y) {
            loseLife();
          }

          if (Math.random() < 0.001 && Date.now() - game.lastEnemyShot > 500) {
            game.enemyBullets.push({ x: enemy.x + 13, y: enemy.y + enemy.height, width: 4, height: 10 });
            game.lastEnemyShot = Date.now();
          }
        }
      });

      game.enemyBullets.forEach((bullet, i) => {
        bullet.y += 5;
        if (bullet.y > canvas.height) {
          game.enemyBullets.splice(i, 1);
        } else {
          ctx.fillStyle = colors[2];
          ctx.fillRect(bullet.x, bullet.y, bullet.width, bullet.height);

          if (!game.invincible &&
              bullet.x < game.player.x + game.player.width &&
              bullet.x + bullet.width > game.player.x &&
              bullet.y < game.player.y + game.player.height &&
              bullet.y + bullet.height > game.player.y) {
            loseLife();
          }
        }
      });

      drawPlayer();

      if (game.enemies.filter(e => e.alive).length === 0) {
        game.enemies = [];
        for (let row = 0; row < 4; row++) {
          for (let col = 0; col < 8; col++) {
            game.enemies.push({
              x: col * 50 + 50,
              y: row * 40 + 50,
              width: 30,
              height: 30,
              alive: true
            });
          }
        }
        game.enemySpeed += 0.5;
      }

      gameLoopRef.current = requestAnimationFrame(update);
    };

    const endGame = () => {
      if (gameLoopRef.current) {
        cancelAnimationFrame(gameLoopRef.current);
      }
      saveScore(username, game.score);
      playAudio('gameover');
      setGameState('gameover');
    };

    const handleKeyDown = (e) => {
      game.keys[e.key] = true;
      if (e.key === ' ') e.preventDefault();
    };

    const handleKeyUp = (e) => {
      game.keys[e.key] = false;
    };

    window.addEventListener('keydown', handleKeyDown);
    window.addEventListener('keyup', handleKeyUp);

    gameDataRef.current = { game, handleKeyDown, handleKeyUp };
    update();
  };

  const startGame = () => {
    if (!username.trim()) {
      alert('Please enter a username');
      return;
    }
    setScore(0);
    setLives(3);
    setGameState('playing');
    playAudio('game');
    setTimeout(initGame, 100);
  };

  const backToMenu = () => {
    if (gameLoopRef.current) {
      cancelAnimationFrame(gameLoopRef.current);
    }
    if (gameDataRef.current) {
      window.removeEventListener('keydown', gameDataRef.current.handleKeyDown);
      window.removeEventListener('keyup', gameDataRef.current.handleKeyUp);
    }
    setGameState('menu');
    playAudio('menu');
  };

  useEffect(() => {
    if (gameState === 'menu') {
      playAudio('menu');
    }
  }, [gameState]);

  useEffect(() => {
    return () => {
      if (gameLoopRef.current) {
        cancelAnimationFrame(gameLoopRef.current);
      }
      if (gameDataRef.current) {
        window.removeEventListener('keydown', gameDataRef.current.handleKeyDown);
        window.removeEventListener('keyup', gameDataRef.current.handleKeyUp);
      }
    };
  }, []);

  return (
    <div className="w-full h-screen bg-black flex items-center justify-center p-4">
      <audio ref={el => audioRefs.current.menu = el} src="menu.mp3" />
      <audio ref={el => audioRefs.current.game = el} src="spaceinvaders.mp3" />
      <audio ref={el => audioRefs.current.gameover = el} src="gameover.mp3" />

      <button
        onClick={() => setMuted(!muted)}
        className="absolute top-4 right-4 bg-gray-800 hover:bg-gray-700 text-white p-3 rounded"
      >
        {muted ? <VolumeX size={24} /> : <Volume2 size={24} />}
      </button>

      {gameState === 'menu' && (
        <div className="bg-gray-900 border-2 border-green-500 p-8 max-w-md w-full">
          <h1 className="text-4xl font-bold text-center mb-8 text-green-500 font-mono">
            SPACE INVADERS
          </h1>
          
          <input
            type="text"
            value={username}
            onChange={(e) => setUsername(e.target.value)}
            placeholder="Enter Username"
            className="w-full p-3 mb-6 bg-black text-green-500 border-2 border-green-500 font-mono"
            maxLength={15}
          />

          <div className="mb-6">
            <p className="text-green-500 text-center mb-3 font-mono">SELECT SHIP</p>
            <div className="flex justify-around">
              {characters.map((char, i) => (
                <button
                  key={i}
                  onClick={() => setSelectedChar(i)}
                  className={`p-4 border-2 transition-all ${
                    selectedChar === i ? 'border-green-500' : 'border-gray-700'
                  }`}
                  style={{ backgroundColor: '#000' }}
                >
                  <div className="w-12 h-12 relative">
                    <div className="absolute inset-0" style={{ backgroundColor: char.colors[0] }}></div>
                    <div className="absolute w-2 h-2 top-2 left-2" style={{ backgroundColor: char.colors[1] }}></div>
                    <div className="absolute w-2 h-2 top-2 right-2" style={{ backgroundColor: char.colors[1] }}></div>
                    <div className="absolute w-4 h-1 bottom-3 left-4" style={{ backgroundColor: char.colors[1] }}></div>
                  </div>
                  <p className="text-green-500 text-xs mt-2 text-center font-mono">{char.name}</p>
                </button>
              ))}
            </div>
          </div>

          <button
            onClick={startGame}
            className="w-full bg-green-500 hover:bg-green-600 text-black font-bold py-4 text-xl mb-6 font-mono"
          >
            START GAME
          </button>

          {leaderboard.length > 0 && (
            <div className="mt-6 border-2 border-green-500 p-4">
              <h3 className="text-green-500 text-center font-bold mb-3 font-mono">HIGH SCORES</h3>
              {leaderboard.map((entry, i) => (
                <div key={i} className="flex justify-between text-green-500 text-sm mb-1 font-mono">
                  <span>{i + 1}. {entry.username}</span>
                  <span>{entry.score}</span>
                </div>
              ))}
            </div>
          )}

          <p className="text-green-500 text-center text-sm mt-4 font-mono">
            Use arrow keys to move and spacebar to shoot
          </p>
        </div>
      )}

      {gameState === 'playing' && (
        <div className="flex flex-col items-center">
          <div className="bg-gray-900 border-2 border-green-500 border-b-0 px-6 py-3 flex justify-between items-center w-full font-mono">
            <p className="text-green-500 text-xl font-bold">SCORE: {score}</p>
            <div className="flex gap-2">
              {[...Array(lives)].map((_, i) => (
                <Heart key={i} className="text-green-500 fill-green-500" size={24} />
              ))}
            </div>
          </div>
          <canvas
            ref={canvasRef}
            width={500}
            height={600}
            className="bg-black border-2 border-green-500"
          />
        </div>
      )}

      {gameState === 'gameover' && (
        <div className="bg-gray-900 border-2 border-green-500 p-8 max-w-md w-full text-center">
          <h1 className="text-4xl font-bold mb-4 text-green-500 font-mono">GAME OVER</h1>
          <p className="text-green-500 text-3xl mb-6 font-mono">SCORE: {score}</p>
          <button
            onClick={backToMenu}
            className="w-full bg-green-500 hover:bg-green-600 text-black font-bold py-4 text-xl font-mono"
          >
            MAIN MENU
          </button>
        </div>
      )}
    </div>
  );
};

export default SpaceInvadersGame;
