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
    <header>
      <div className={styles["header-logo"]}>
        <img src={logoSvg} className={styles.appLogo} onClick={() => window.location.reload()} alt="logo" />
        <input
          value={searchItem}
          onChange={handleSearchChange}
          placeholder="Search by name, SID, or title"
        />
      </div>
      <button onClick={onToggleCompare} className="btn btn-primary">
        {showCompare ? "Hide Compare" : "Compare Employees"}
      </button>
      <h1 className={styles.appHeading} onClick={() => window.location.reload()}>
        JPMorganChase
      </h1>
    </header>
  );
}

function Dashboard() {
  const totalEmployees = myUsers.length;
  const averageExperience = myUsers.reduce((sum, user) => sum + user.yearsOfExperience, 0) / totalEmployees;

  return (
    <div className="dashboard">
      <p>Total Employees: {totalEmployees}</p>
      {/* Add more statistics as needed */}
    </div>
  );
}

export default function MainSearchApp() {
  const [showCompare, setShowCompare] = useState(false);
  const [searchItem, setSearchItem] = useState('');
  const [filteredUsers, setFilteredUsers] = useState<User[]>(myUsers);
  const [showResult, setShowResult] = useState(false);
  const [currentId, setCurrentId] = useState(0);

  // Configure Fuse.js options
  const fuseOptions = {
    keys: ['name', 'sid', 'title'],
    threshold: 0.3, // Adjust this value to control the fuzziness
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
    <div className={styles.appContainer}>
      <Header
        searchItem={searchItem}
        onSearchChange={setSearchItem}
        onToggleCompare={() => setShowCompare(!showCompare)}
        showCompare={showCompare}
      />
      {/*<Dashboard />*/}

      {showResult ? (
        <div className="employee-profile py-4">
          {/* Your unchanged profile rendering code goes here */}
          {/* ... */}
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
        </div>
      )}
      {showCompare && <CompareEmployees />}
    </div>
  );
}

import React, { useState, useEffect } from 'react';
import { BarChart, Bar, XAxis, YAxis, Tooltip, ResponsiveContainer } from 'recharts';
import employeesData from './employees.json';
import {Card, CardContent} from "./card";
import styles from './App.module.scss';
import 'bootstrap/dist/css/bootstrap.css';

export default function CompareEmployees() {

  type TopEvent = {
    name: string;
    count: number;
  };

  type CommonalityItem = {
    name: string;
    shared: string[];
  };

  type EventData = { name: string; count: number };
  const [topEvents, setTopEvents] = useState<TopEvent[]>([]);

  type Commonality = { name: string; count: number };
  const [commonalities, setCommonalities] = useState<CommonalityItem[]>([]);

  const [selectedId, setSelectedId] = useState('');


  useEffect(() => {
    const eventMap = new Map<string, number>();
    employeesData.forEach((emp) => {
      emp.events?.forEach((event) => {
        if (event.rsvped) {
          const currentCount = eventMap.get(event.name) ?? 0;
          eventMap.set(event.name, currentCount + 1);
        }
      });
    });
    const chartData = Array.from(eventMap.entries()).map(([name, count]) => ({name, count}));
    setTopEvents(chartData);
  }, []);

  const findCommonalities = (id: string) => {
    const person = employeesData.find((e) => e.id === parseInt(id));
    if (!person) return;

    const results = employeesData
      .filter((e) => e.id !== person.id)
      .map((other) => {
        const shared = [];
        if (other.university === person.university) shared.push('University');
        if (other.major === person.major) shared.push('Major');
        if (other.lineOfBusiness === person.lineOfBusiness) shared.push('Line of Business');
        if (person.hobbies.some((h) => other.hobbies.includes(h))) shared.push('Hobbies');
        if (person.groups?.some((g) => other.groups?.includes(g))) shared.push('Groups');
        return {name: other.name, shared};
      })
      .filter((entry) => entry.shared.length > 0);

    setCommonalities(results);
  };

  return (
    <div className="p-4">
      <div className="p-6 space-y-6">
        <h1 className="text-2xl font-bold text-[#003F5F]">JPMorgan Chase Employee Dashboard</h1>

        <Card>
          <CardContent className="p-4">
            <h2 className="text-xl font-semibold mb-2">Top RSVPed Events</h2>
            <ResponsiveContainer width="100%" height={300}>
              <BarChart data={topEvents}>
                <XAxis dataKey="name" tick={{fontSize: 12}} interval={0} angle={-20} textAnchor="end" height={80}/>
                <YAxis allowDecimals={false}/>
                <Tooltip/>
                <Bar dataKey="count" fill="#0072C6"/>
              </BarChart>
            </ResponsiveContainer>
          </CardContent>
        </Card>

        <Card>
          <CardContent className="p-4">
            <h2 className="text-xl font-semibold mb-2">Find Commonalities</h2>
            <select
              className="border p-2 rounded w-full mb-4"
              value={selectedId}
              onChange={(e) => {
                setSelectedId(e.target.value);
                findCommonalities(e.target.value);
              }}
            >
              <option value="">Select an employee</option>
              {employeesData.map((emp) => (
                <option key={emp.id} value={emp.id}>
                  {emp.name}
                </option>
              ))}
            </select>

            {commonalities.length > 0 && (
              <ul className="list-disc list-inside">
                {commonalities.map((c, index) => (
                  <li key={index}>
                    <strong>{c.name}:</strong> {c.shared.join(', ')}
                  </li>
                ))}
              </ul>
            )}
          </CardContent>
        </Card>
      </div>
      {/* Your compare logic goes here */}
    </div>
  );
};


@tailwind base;
@tailwind components;
@tailwind utilities;

$chase-blue: #0072c6;
$hover-gray: #e0e0e0;
$text-dark: #333;
$bg-light: #f8f8f8;

body {
  margin: 0;
  font-family: 'Segoe UI', 'Roboto',sans-serif;
  background: linear-gradient(to bottom right, #f5f7fa, #e4e7eb);

  color: #1a1a1a;

}

header {
  position: fixed;
  top: 0; left: 0;
  width: 100%;
  background-color: #003a6d;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
  padding: 10px 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  z-index: 1000;

  .header-logo {
    display: flex;
    align-items: center;
    gap: 10px;

    img {
      width: 3vw;
      pointer-events: none;
      animation: app-logo-spin infinite 20s linear;
    }
  }

  h1 {
    font-size: 2.5rem;
    font-family: 'Libre Baskerville', serif;

    -webkit-background-clip: text;
    color: white;
    margin: 0;
    cursor: pointer;
  }
}

@keyframes app-logo-spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.appContainer {
  text-align: center;
  min-height: 100vh;
  padding-top: 80px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.appLink {
  color: $chase-blue;
  text-decoration: underline;
  cursor: pointer;
}

.back-btn {
  color: $chase-blue;
  cursor: pointer;
  font-weight: bold;
  margin-bottom: 15px;
  display: inline-block;
}

.profile_img {
  width: 150px;
  height: 150px;
  object-fit: cover;
  border-radius: 50%;
  margin-bottom: 10px;
}

.employee-profile {
  .card-header {
    text-align: center;
  }

  .table th, .table td {
    font-size: 14px;
    padding: 10px;
  }
}

.card {
  transition: transform 0.2s, box-shadow 0.2s;
  &:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0,0,0,0.15);
  }
}






