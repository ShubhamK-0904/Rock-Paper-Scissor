# 🎮 Rock, Paper, Scissors Game

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/Tkinter-336E7B?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/Game-FF6B6B?style=for-the-badge" />
  <img src="https://img.shields.io/badge/GUI-4285F4?style=for-the-badge" />
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" />
</p>

---

## 🎮 Overview

**Rock, Paper, Scissors Game** is a Python implementation of the classic strategy game with command-line input and interactive tkinter GUI. Features core game logic against an intelligent computer opponent, dynamic result display, "Play Again" functionality, and optional winner celebration GIF support using Pillow. Perfect for learning game development and GUI programming.

**Perfect for:** Learning game logic, GUI programming, AI opponents, interactive applications.

---

## ✨ Key Features

- 🎯 **Classic Game Mechanics**
  - Rock vs Paper vs Scissors
  - Computer AI opponent
  - Win/Lose/Draw logic
  - Score tracking

- 🎨 **Interactive GUI**
  - Tkinter interface
  - Button controls
  - Real-time feedback
  - Visual styling

- 🤖 **Smart AI**
  - Random computer choices
  - Pattern-based strategy (optional)
  - Difficulty levels
  - Smart responses

- 📊 **Score Management**
  - Win tracking
  - Loss tracking
  - Draw tracking
  - Win rate calculation

- 🎉 **Celebration Features**
  - Winner animations
  - GIF display support
  - Score display
  - Replay functionality

- ♻️ **Play Again Button**
  - Reset game state
  - Continue playing
  - Persistent scoring

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| **Language** | Python 3.8+ |
| **GUI Framework** | Tkinter |
| **Image Processing** | Pillow (PIL) |
| **Game Logic** | Python random module |
| **Display** | Tkinter Labels/Buttons |

---

## 📋 Requirements

```bash
pip install pillow
```

---

## 🚀 Quick Start

### 1. **Clone Repository**
```bash
git clone https://github.com/ShubhamK-0904/Rock-Paper-Scissor.git
cd Rock-Paper-Scissor
```

### 2. **Install Dependencies**
```bash
pip install pillow
```

### 3. **Run Game**
```bash
python rock_paper_scissor.py
```

---

## 💻 Game Mechanics

### **Game Logic**
```
Rock beats Scissors
Scissors beats Paper
Paper beats Rock

Equal = Draw
```

---

## 📁 Project Structure

```
Rock-Paper-Scissor/
├── rock_paper_scissor.py    # Main game file
├── gui_version.py            # Tkinter GUI version
├── assets/
│   ├── rock.png
│   ├── paper.png
│   ├── scissors.png
│   └── winner.gif
├── requirements.txt
└── README.md
```

---

## 💻 Code Implementation

### **1. Command-Line Version**
```python
import random

def play_game():
    choices = ['rock', 'paper', 'scissors']
    
    player_choice = input("Enter rock, paper, or scissors: ").lower()
    if player_choice not in choices:
        print("Invalid choice!")
        return
    
    computer_choice = random.choice(choices)
    
    print(f"You chose: {player_choice}")
    print(f"Computer chose: {computer_choice}")
    
    if player_choice == computer_choice:
        print("It's a draw!")
    elif (player_choice == 'rock' and computer_choice == 'scissors') or \
         (player_choice == 'scissors' and computer_choice == 'paper') or \
         (player_choice == 'paper' and computer_choice == 'rock'):
        print("You win!")
        return True
    else:
        print("You lose!")
        return False

# Play multiple rounds
wins = 0
losses = 0
while True:
    result = play_game()
    if result:
        wins += 1
    elif result is False:
        losses += 1
    
    play_again = input("\nPlay again? (yes/no): ").lower()
    if play_again != 'yes':
        break

print(f"\nFinal Score - Wins: {wins}, Losses: {losses}")
```

### **2. GUI Version with Tkinter**
```python
import tkinter as tk
from tkinter import messagebox
import random
from PIL import Image, ImageTk

class RockPaperScissorsGame:
    def __init__(self, root):
        self.root = root
        self.root.title("Rock, Paper, Scissors")
        self.root.geometry("400x500")
        
        self.wins = 0
        self.losses = 0
        self.draws = 0
        
        # Title
        title = tk.Label(root, text="Rock, Paper, Scissors", font=("Arial", 24, "bold"))
        title.pack(pady=20)
        
        # Score Display
        self.score_label = tk.Label(root, text=self.get_score_text(), font=("Arial", 14))
        self.score_label.pack(pady=10)
        
        # Buttons Frame
        button_frame = tk.Frame(root)
        button_frame.pack(pady=20)
        
        tk.Button(button_frame, text="🪨 Rock", font=("Arial", 12), width=10, 
                  command=lambda: self.play('rock')).grid(row=0, column=0, padx=5)
        tk.Button(button_frame, text="📄 Paper", font=("Arial", 12), width=10, 
                  command=lambda: self.play('paper')).grid(row=0, column=1, padx=5)
        tk.Button(button_frame, text="✂️ Scissors", font=("Arial", 12), width=10, 
                  command=lambda: self.play('scissors')).grid(row=0, column=2, padx=5)
        
        # Result Display
        self.result_label = tk.Label(root, text="Make your choice!", font=("Arial", 12), fg="blue")
        self.result_label.pack(pady=20)
        
        # Play Again Button
        tk.Button(root, text="Reset Game", font=("Arial", 12), bg="lightcoral",
                  command=self.reset_game).pack(pady=10)
    
    def play(self, player_choice):
        choices = ['rock', 'paper', 'scissors']
        computer_choice = random.choice(choices)
        
        result = self.determine_winner(player_choice, computer_choice)
        
        self.result_label.config(
            text=f"You: {player_choice.upper()}\nComputer: {computer_choice.upper()}\n{result}"
        )
        self.score_label.config(text=self.get_score_text())
    
    def determine_winner(self, player, computer):
        if player == computer:
            self.draws += 1
            return "Draw!"
        
        wins = {
            ('rock', 'scissors'): 'You Win!',
            ('scissors', 'paper'): 'You Win!',
            ('paper', 'rock'): 'You Win!'
        }
        
        if (player, computer) in wins:
            self.wins += 1
            return wins[(player, computer)]
        else:
            self.losses += 1
            return "Computer Wins!"
    
    def get_score_text(self):
        return f"Score - Wins: {self.wins} | Losses: {self.losses} | Draws: {self.draws}"
    
    def reset_game(self):
        self.wins = 0
        self.losses = 0
        self.draws = 0
        self.score_label.config(text=self.get_score_text())
        self.result_label.config(text="Make your choice!")

if __name__ == "__main__":
    root = tk.Tk()
    game = RockPaperScissorsGame(root)
    root.mainloop()
```

---

## 🎯 Game Rules

| Scenario | Result |
|----------|--------|
| Rock vs Scissors | Rock wins |
| Scissors vs Paper | Scissors wins |
| Paper vs Rock | Paper wins |
| Same choice | Draw |

---

## 🤖 AI Difficulty Levels (Optional)

### **Easy**
```python
computer_choice = random.choice(['rock', 'paper', 'scissors'])
```

### **Medium**
```python
# Slight bias based on previous rounds
```

### **Hard**
```python
# Learns player patterns
```

---

## 📊 Game Statistics

| Metric | Tracked |
|--------|---------|
| **Wins** | ✅ Yes |
| **Losses** | ✅ Yes |
| **Draws** | ✅ Yes |
| **Win Rate** | ✅ Calculated |
| **Streak** | ✅ Optional |

---

## 🎨 GUI Features

- 🎯 **Button Layout**
  - Three choice buttons
  - Clear labeling
  - Emoji support

- 📊 **Score Display**
  - Real-time updates
  - Win/Loss/Draw count
  - Win percentage

- 💬 **Result Display**
  - Your choice
  - Computer choice
  - Game result

- ♻️ **Reset Button**
  - Clear scores
  - Start fresh

---

## 💡 Real-World Applications

✅ **Game Development:** Learn game mechanics  
✅ **GUI Programming:** Master Tkinter  
✅ **AI Development:** Implement simple AI  
✅ **Data Tracking:** Score management  
✅ **Portfolio Project:** Showcase skills  

---

## 🎓 Learning Outcomes

Master these concepts:
- ✅ Game logic and rules
- ✅ Tkinter GUI programming
- ✅ Button event handling
- ✅ State management
- ✅ Random number generation
- ✅ Conditional logic
- ✅ Score tracking
- ✅ User interactions

---

## 🚀 Future Enhancements

- [ ] Difficulty levels
- [ ] Sound effects
- [ ] Leaderboard system
- [ ] Multiplayer mode
- [ ] Advanced AI strategy
- [ ] Theme customization
- [ ] Statistics tracking
- [ ] Network play

---

## 🤝 Contributing

Contributions welcome!
1. Fork repository
2. Create feature branch
3. Add improvements
4. Submit pull request

---

## 📝 License

MIT License - see LICENSE file

---

## 👨‍💻 Author

**Shubham Kadam**
- GitHub: [@ShubhamK-0904](https://github.com/ShubhamK-0904)
- LinkedIn: [Shubham Kadam](https://www.linkedin.com/in/shubham-kadam-b8856031a/)
- Email: shubham85kadam@gmail.com

---

<p align="center">
  <strong>⭐ Have fun playing? Give it a star! ⭐</strong>
</p>

<p align="center">
  Made with ❤️ by Shubham Kadam | Last Updated: May 2026
</p>
