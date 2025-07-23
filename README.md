# Top-Down Zombie Shooter Game

This project is a top-down 2D zombie survival game where the player must fend off waves of zombies using a shotgun. Players can move, aim, shoot, and survive for as long as possible while trying to achieve a high score. The game uses basic 2D graphics and animations to provide an engaging and dynamic experience.

<img src="https://github.com/user-attachments/assets/94b4a62e-39e7-489c-8d99-fcd3b9acc6a6" alt="Screenshot 1" width="400">
<img src="https://github.com/user-attachments/assets/a1819c6f-8e08-4d76-b265-ae6f945225b6" alt="Screenshot 2" width="400">
<img src="https://github.com/user-attachments/assets/06ec32b8-4a16-4067-bc27-4e483e7e0421" alt="Screenshot 3" width="400">
<img src="https://github.com/user-attachments/assets/03396b12-17c6-4aa4-ba44-1c4c74786699" alt="Screenshot 4" width="400">


## Features

- **Player Movement**: Move forward and backward while rotating the character using the mouse.
- **Shooting**: Aim with the mouse and shoot bullets to kill zombies.
- **Infinite Grass**: Dynamic background with endless grass terrain as the player moves.
- **Zombies**: Spawn, chase, and attack the player with animated zombie sprites.
- **Animations**: Player and zombie have idle, movement, and attack animations.
- **Crosshair**: Dynamic crosshair follows mouse movement.
- **Score System**: Track current score and high score.
- **Game Over Screen**: Display high score after the game ends.
- **Responsive Controls**: Supports mouse controls for shooting and keyboard controls for movement.

## Gameplay

- Move the player using `W`, `A`, `S`, `D` or the arrow keys.
- Aim with the mouse.
- Left-click to shoot at zombies.
- Survive as long as possible and try to achieve the highest score.
- When hit by a zombie, the game ends and shows the "Game Over" screen with the player's high score.

## Controls

- **Move Forward**: `W` / `Up Arrow`
- **Move Backward**: `S` / `Down Arrow`
- **Move Left**: `A` / `Left Arrow`
- **Move Right**: `D` / `Right Arrow`
- **Shoot**: `Left Mouse Button`
- **Aim**: Mouse movement

## Assets

The game uses sprite sheets for both player and zombie animations:
- **Player animations**: Idle, move, and shoot with a shotgun.
- **Zombie animations**: Movement and attack animations.

### Images
- **Player Sprite**: `images/Top_Down_Survivor/shotgun/idle/`
- **Zombie Sprite**: `images/tds_zombie/export/`
- **Grass Background**: `images/grass.png`
- **Bullet**: `images/bullet.png`
- **Crosshair**: `images/crosshair097.png`
- **Game Over Screen**: `images/Game Over.png`

## Installation and Setup

1. Clone or download the repository.
2. Open the index.html file in a browser.
3. Start the game by interacting with the canvas.

## Link to the game

Link to the game online: https://berhanewhe5.github.io/JavaScript-Top-Down-Shooter/

## Credits

1. All Code by Berhane Wheeler
2. Zombie sprite: https://opengameart.org/content/animated-top-down-zombie
3. Player sprite: https://opengameart.org/content/animated-top-down-survivor-player
4. Grass sprite: https://opengameart.org/content/grass-texture-pack



------------
import logoSvg from './logo.svg';
import styles from './App.module.scss';
import { useEffect, useState } from 'react';
import myUsers from './employees.json';
import 'bootstrap/dist/css/bootstrap.css';
import '@mds/react';
import { MdsSearchBox } from "@mds/react";
import Fuse from 'fuse.js';
type User = typeof myUsers[number];
import CompareEmployees from './CompareEmployees';

function Header({ searchItem, onSearchChange, onToggleCompare, showCompare }: { searchItem: string; onSearchChange: (value: string) => void; onToggleCompare: () => void; showCompare: boolean; }) {
  const handleSearchChange = (event: any) => {
    const searchValue = event.target?.value || event.value || '';
    onSearchChange(searchValue);
  };

  return (
    <div className={styles["header-logo"]}>
      <img
        src={logoSvg}
        className={styles.appLogo}
        onClick={() => window.location.reload()}
        alt="logo"
      />
      <h1 className={styles.appHeading} onClick={() => window.location.reload()}>
        JPMorganChase
      </h1>
      {!searchItem && (
        <button onClick={onToggleCompare} className="btn btn-primary ms-3">
          {showCompare ? "Hide Compare" : "Compare Employees"}
        </button>
      )}
    </div>
  );
}

function Dashboard() {
  const totalEmployees = myUsers.length;
  const averageExperience = myUsers.reduce((sum, user) => sum + user.yearsOfExperience, 0) / totalEmployees;

  return (
    <div>
      Total Employees: {totalEmployees}
      <br />
      Average Experience: {averageExperience.toFixed(1)} years
    </div>
  );
}

export default function MainSearchApp() {
  const [showCompare, setShowCompare] = useState(false);
  const [searchItem, setSearchItem] = useState('');
  const [filteredUsers, setFilteredUsers] = useState<User[]>(myUsers);
  const [showResult, setShowResult] = useState(false);
  const [currentId, setCurrentId] = useState(0);

  const fuseOptions = {
    keys: ['name', 'sid', 'title'],
    threshold: 0.3,
  };

  const fuse = new Fuse(myUsers, fuseOptions);

  useEffect(() => {
    if (searchItem) {
      const results = fuse.search(searchItem);
      setFilteredUsers(results.map(result => result.item));
    } else {
      setFilteredUsers(myUsers);
    }
  }, [searchItem]);

  const handleInputChange = (value: string) => {
    setSearchItem(value);
    setShowResult(false);
  };

  const displayResult = (userId: number) => {
    setCurrentId(userId - 1);
    setShowResult(true);
  };

  const user = myUsers[currentId];
  const manager = user?.managerId ? myUsers[user.managerId - 1] : null;

  return (
    <>
      <Header
        searchItem={searchItem}
        onSearchChange={setSearchItem}
        onToggleCompare={() => setShowCompare(!showCompare)}
        showCompare={showCompare}
      />

      {showResult ? (
        <div className="employee-profile py-4 container">
          <h2>{user.name}</h2>
          <p><strong>SID:</strong> {user.sid}</p>
          <p><strong>Title:</strong> {user.title}</p>
          <p><strong>Phone:</strong> {user.cellPhone}</p>
          <p><strong>University:</strong> {user.university}</p>
          <p><strong>Major:</strong> {user.major}</p>
          <p><strong>RSVPed Events:</strong> {user.events?.filter(e => e.rsvped).map(e => e.name).join(', ') || 'None'}</p>
          <p><strong>Groups:</strong> {user.groups?.join(', ') || 'None'}</p>
          {manager && <p><strong>Manager:</strong> {manager.name}</p>}
        </div>
      ) : (
        <div className="container mt-4">
          {searchItem ? (
            filteredUsers.length ? (
              <div className="row">
                {filteredUsers.map(u => (
                  <div key={u.id} className="col-md-4 mb-3">
                    <div
                      className="card shadow-sm"
                      onClick={() => displayResult(u.id)}
                      style={{ cursor: 'pointer' }}
                    >
                      <div className="card-body text-center">
                        <img
                          src={u.image}
                          alt={u.name}
                          className="rounded-circle mb-2"
                          width="60"
                          height="60"
                        />
                        <h5 className="card-title">{u.name}</h5>
                        <p className="card-text">{u.title}</p>
                        <small>{u.sid}</small>
                      </div>
                    </div>
                  </div>
                ))}
              </div>
            ) : (
              <p>No results for "{searchItem}".</p>
            )
          ) : (
            <p>Start typing to search employees.</p>
          )}

          {showCompare && <div className="mt-5"><CompareEmployees /></div>}
        </div>
      )}
    </>
  );
}
