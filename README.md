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

function Header({
  searchItem,
  onSearchChange,
  onToggleCompare,
  showCompare,
}: {
  searchItem: string;
  onSearchChange: (value: string) => void;
  onToggleCompare: () => void;
  showCompare: boolean;
}) {
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
        <button className="btn btn-outline-primary" onClick={onToggleCompare}>
          {showCompare ? "Hide Compare" : "Compare Employees"}
        </button>
      )}
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

  const displaySearch = () => setShowResult(false);

  const user = myUsers[currentId];
  const manager = user?.managerId ? myUsers[user.managerId - 1] : null;

  return (
    <>
      <Header
        searchItem={searchItem}
        onSearchChange={setSearchItem}
        onToggleCompare={() => setShowCompare(!showCompare)}
        showCompare={showCompare && !searchItem && !showResult}
      />

      {showResult ? (
        <div className="employee-profile py-4">
          <div className="container">
            <span className={styles["back-btn"]} onClick={displaySearch}>← Back</span>
            <div className="row mt-3">
              <div className="col-lg-4 mb-4">
                <div className="card shadow-sm">
                  <div className="card-header text-center">
                    <img src={user.image} alt={user.name} className={`profile_img rounded-circle`} />
                    <h3>{user.name} ({user.pronouns})</h3>
                  </div>
                  <div className="card-body">
                    <p><strong>Title:</strong> {user.title}</p>
                    <p><strong>SID:</strong> {user.sid}</p>
                    <p><strong>Manager:</strong> {manager
                      ? <span className={styles.appLink} onClick={() => displayResult(manager.id)}>{manager.name}</span>
                      : 'N/A'}</p>
                  </div>
                </div>
              </div>

              <div className="col-lg-8">
                <div className="card shadow-sm mb-4">
                  <div className="card-header"><h4>General Info</h4></div>
                  <div className="card-body">
                    <table className="table table-bordered">
                      <tbody>
                        <tr><th>Email</th><td>{user.email}</td></tr>
                        <tr><th>Cellphone</th><td>{user.cellPhone}</td></tr>
                        <tr><th>Company</th><td>{user.company}</td></tr>
                        <tr><th>LOB</th><td>{user.lineOfBusiness}</td></tr>
                        <tr><th>Address</th><td>{user.address}</td></tr>
                      </tbody>
                    </table>
                  </div>
                </div>

                <div className="card shadow-sm mb-4">
                  <div className="card-header"><h4>Career Profile</h4></div>
                  <div className="card-body">
                    <p>{user.story}</p>
                    <table className="table table-bordered">
                      <tbody>
                        <tr><th>Experience</th><td>{user.yearsOfExperience}</td></tr>
                        <tr><th>University</th><td>{user.university}</td></tr>
                        <tr><th>Major</th><td>{user.major}</td></tr>
                        <tr><th>LinkedIn</th><td><a href={user.linkedin} target="_blank">{user.linkedin}</a></td></tr>
                        <tr><th>Hobbies</th><td>{user.hobbies.join(', ')}</td></tr>
                      </tbody>
                    </table>
                  </div>
                </div>

                <div className="card shadow-sm mb-4">
                  <div className="card-header"><h4>Past Projects</h4></div>
                  <div className="card-body">
                    <ul>{user.pastProjects.map((p, i) => <li key={i}>{p}</li>)}</ul>
                  </div>
                </div>

                <div className="card shadow-sm mb-4">
                  <div className="card-header"><h4>RSVPed Events</h4></div>
                  <div className="card-body">
                    <ul>{user.events?.filter(e => e.rsvped).map((event, i) => (
                      <li key={i}>{event.name}</li>
                    ))}</ul>
                  </div>
                </div>

                <div className="card shadow-sm">
                  <div className="card-header"><h4>Groups</h4></div>
                  <div className="card-body">
                    <ul>{user.groups?.map((group, i) => <li key={i}>{group}</li>)}</ul>
                  </div>
                </div>

              </div>
            </div>
          </div>
        </div>
      ) : (
        <div className="container mt-4">
          {searchItem ? (
            filteredUsers.length ? (
              <div className="row">
                {filteredUsers.map(u => (
                  <div key={u.id} className="col-md-4 mb-3">
                    <div className="card shadow-sm" onClick={() => displayResult(u.id)} style={{ cursor: 'pointer' }}>
                      <div className="card-body text-center">
                        <img src={u.image} alt={u.name} className="rounded-circle mb-2" width="60" height="60" />
                        <h5 className="card-title">{u.name}</h5>
                        <p className="card-text">{u.title}</p>
                        <small>{u.sid}</small>
                      </div>
                    </div>
                  </div>
                ))}
              </div>
            ) : <p>No results for "{searchItem}".</p>
          ) : (
            <>
              <p>Start typing to search employees.</p>
              {showCompare && (
                <CompareEmployees onSelectEmployee={(id) => {
                  setCurrentId(id - 1);
                  setShowResult(true);
                }} />
              )}
            </>
          )}
        </div>
      )}
    </>
  );
}
✅ Last Step — Update CompareEmployees.tsx to support name click:
Modify CompareEmployees like this:

tsx
Copy
Edit
export default function CompareEmployees({ onSelectEmployee }: { onSelectEmployee: (id: number) => void }) {
  const commonalities = [...]; // however you're computing this

  return (
    <div className="card shadow-sm mt-4">
      <div className="card-header"><h4>Find Commonalities</h4></div>
      <div className="card-body">
        <ul style={{ listStyleType: 'none', paddingLeft: 0 }}>
          {commonalities.map((c, index) => (
            <li key={index}>
              <span
                style={{ color: "#0072c6", cursor: "pointer", fontWeight: "bold" }}
                onClick={() => {
                  const user = myUsers.find(u => u.name === c.name);
                  if (user) onSelectEmployee(user.id);
                }}
              >
                {c.name}
              </span>
              : {c.shared.join(', ')}
            </li>
          ))}
        </ul>
      </div>
    </div>
  );
}
