// Guitar Learning Path Application
const levelsData = [
    {
        number: 1,
        title: "Foundations",
        description: "Essential basics and first steps",
        difficulty: "beginner",
        topics: [
            {
                name: "Guitar Basics",
                items: ["Guitar anatomy and parts", "Proper posture and pick holding", "Tuning fundamentals"]
            },
            {
                name: "Open Chords",
                items: ["Learn C, G, D, Em, Am chords", "Practice chord transitions", "Basic chord progressions"]
            },
            {
                name: "Strumming & Rhythm",
                items: ["Master downstrokes", "Simple down-up patterns", "4/4 time counting"]
            },
            {
                name: "First Songs",
                items: ["2-chord progressions", "3-chord songs", "Build playing confidence"]
            },
            {
                name: "Practice Methods",
                items: ["Using a metronome", "Slow practice technique", "Clean chord changes"]
            }
        ]
    },
    {
        number: 2,
        title: "Technique Development",
        description: "Building skills and music theory",
        difficulty: "beginner",
        topics: [
            {
                name: "Finger Independence",
                items: ["Chromatic exercises", "Finger strength drills"]
            },
            {
                name: "Fingerpicking Basics",
                items: ["Travis picking pattern", "Alternating bass notes", "Thumb and finger coordination"]
            },
            {
                name: "Music Theory Foundation",
                items: ["Fretboard notes (E and A strings)", "Understanding intervals", "Major and pentatonic scales"]
            },
            {
                name: "Ear Training",
                items: ["Major vs minor recognition", "Basic melodic patterns", "Chord quality identification"]
            }
        ]
    },
    {
        number: 3,
        title: "Chord Expansion",
        description: "Advanced chords and techniques",
        difficulty: "intermediate",
        topics: [
            {
                name: "Barre Chords",
                items: ["F major barre chord", "B minor shape", "Movable chord forms"]
            },
            {
                name: "Extended Chords",
                items: ["Seventh chords (maj7, m7, dom7)", "Suspended chords", "Add9 variations"]
            },
            {
                name: "Rhythmic Complexity",
                items: ["Syncopated strumming", "Palm muting technique", "Dynamic accents"]
            },
            {
                name: "Hybrid Techniques",
                items: ["Fingerpicking + strumming", "Percussive elements", "Chord melody basics"]
            },
            {
                name: "Riffs and Fills",
                items: ["Common acoustic riffs", "Transitional phrases", "Melodic embellishments"]
            }
        ]
    },
    {
        number: 4,
        title: "Song Application",
        description: "Full songs and jamming skills",
        difficulty: "intermediate",
        topics: [
            {
                name: "Complete Songs",
                items: ["Multi-chord progressions", "Genre variety", "Performance pieces"]
            },
            {
                name: "Jamming Skills",
                items: ["Backing track practice", "Improvisation basics", "Call and response"]
            },
            {
                name: "Advanced Listening",
                items: ["Song transcription", "Chord progression analysis", "Melody extraction"]
            },
            {
                name: "Creative Development",
                items: ["Alternate tunings", "Basic songwriting", "Recording practice", "Self-assessment skills"]
            }
        ]
    },
    {
        number: 5,
        title: "Advanced Mastery",
        description: "Professional techniques and style",
        difficulty: "advanced",
        topics: [
            {
                name: "Advanced Fingerstyle",
                items: ["Complex picking patterns", "Percussive techniques", "Multi-voice arrangements"]
            },
            {
                name: "Complex Rhythms",
                items: ["Odd time signatures", "Polyrhythmic concepts", "Advanced syncopation"]
            },
            {
                name: "Lead Guitar",
                items: ["Scale applications", "Solo construction", "Melodic development"]
            },
            {
                name: "Style Mastery",
                items: ["Blues fingerstyle", "Folk arrangements", "Pop acoustic styles"]
            },
            {
                name: "Performance",
                items: ["Stage presence", "Creative expression", "Professional skills"]
            }
        ]
    }
];

// In-memory progress storage (note: will not persist between page reloads)
let progress = {};
let totalItems = 0;

// Generate level HTML
function generateLevels() {
    const container = document.getElementById('levelsContainer');
    container.innerHTML = '';
    totalItems = 0;
    
    levelsData.forEach(level => {
        // Count total items
        level.topics.forEach(topic => {
            totalItems += topic.items.length;
        });
        
        const levelEl = document.createElement('div');
        levelEl.className = 'level';
        levelEl.id = `level-${level.number}`;
        
        levelEl.innerHTML = `
            <div class="level-header" onclick="toggleLevel(${level.number})">
                <div class="level-title-section">
                    <div class="level-number">${level.number}</div>
                    <div class="level-info">
                        <div class="level-name">Level ${level.number}: ${level.title}</div>
                        <div class="level-description">${level.description}</div>
                    </div>
                </div>
                <div class="level-meta">
                    <span class="level-badge badge-${level.difficulty}">${level.difficulty}</span>
                    <span class="level-progress" id="progress-${level.number}">0/0</span>
                    <span class="chevron">▼</span>
                </div>
            </div>
            <div class="level-content">
                <div class="level-body">
                    ${level.topics.map(topic => `
                        <div class="topic">
                            <div class="topic-name">${topic.name}</div>
                            <div class="topic-items">
                                ${topic.items.map((item, index) => `
                                    <div class="topic-item" onclick="toggleItem('${level.number}-${topic.name}-${index}')">
                                        <div class="checkbox"></div>
                                        <div class="item-text">${item}</div>
                                    </div>
                                `).join('')}
                            </div>
                        </div>
                    `).join('')}
                </div>
            </div>
        `;
        
        container.appendChild(levelEl);
    });
    
    updateAllProgress();
}

// Toggle level expand/collapse
function toggleLevel(levelNumber) {
    const level = document.getElementById(`level-${levelNumber}`);
    level.classList.toggle('open');
}

// Toggle item completion
function toggleItem(itemId) {
    // Find the clicked item using a more specific selector
    const allItems = document.querySelectorAll('.topic-item');
    let clickedItem = null;
    
    allItems.forEach(item => {
        const onclick = item.getAttribute('onclick');
        if (onclick && onclick.includes(`'${itemId}'`)) {
            clickedItem = item;
        }
    });
    
    if (!clickedItem) return;
    
    const checkbox = clickedItem.querySelector('.checkbox');
    
    if (progress[itemId]) {
        // Uncheck item
        delete progress[itemId];
        checkbox.classList.remove('checked');
        clickedItem.classList.remove('completed');
    } else {
        // Check item
        progress[itemId] = true;
        checkbox.classList.add('checked');
        clickedItem.classList.add('completed');
    }
    
    updateAllProgress();
    checkLevelCompletion(itemId.split('-')[0]);
}

// Update all progress displays
function updateAllProgress() {
    const completed = Object.keys(progress).filter(key => !key.includes('-completed')).length;
    const percentage = totalItems > 0 ? (completed / totalItems) * 100 : 0;
    
    // Update overall progress
    document.getElementById('progressFill').style.width = `${percentage}%`;
    document.getElementById('completedCount').textContent = completed;
    document.getElementById('totalCount').textContent = totalItems;
    
    // Update item states
    Object.keys(progress).forEach(itemId => {
        if (itemId.includes('-completed')) return;
        
        const allItems = document.querySelectorAll('.topic-item');
        allItems.forEach(item => {
            const onclick = item.getAttribute('onclick');
            if (onclick && onclick.includes(`'${itemId}'`)) {
                const checkbox = item.querySelector('.checkbox');
                checkbox.classList.add('checked');
                item.classList.add('completed');
            }
        });
    });
    
    // Update level progress
    levelsData.forEach(level => {
        let levelTotal = 0;
        let levelCompleted = 0;
        
        level.topics.forEach(topic => {
            topic.items.forEach((item, index) => {
                levelTotal++;
                const itemId = `${level.number}-${topic.name}-${index}`;
                if (progress[itemId]) levelCompleted++;
            });
        });
        
        const progressEl = document.getElementById(`progress-${level.number}`);
        if (progressEl) {
            progressEl.textContent = `${levelCompleted}/${levelTotal}`;
        }
        
        const levelEl = document.getElementById(`level-${level.number}`);
        if (levelEl) {
            if (levelCompleted === levelTotal && levelTotal > 0) {
                levelEl.classList.add('completed');
            } else {
                levelEl.classList.remove('completed');
            }
        }
    });
}

// Check if level is completed and show modal
function checkLevelCompletion(levelNumber) {
    const level = levelsData.find(l => l.number == levelNumber);
    if (!level) return;
    
    let levelTotal = 0;
    let levelCompleted = 0;
    
    level.topics.forEach(topic => {
        topic.items.forEach((item, index) => {
            levelTotal++;
            const itemId = `${level.number}-${topic.name}-${index}`;
            if (progress[itemId]) levelCompleted++;
        });
    });
    
    const completionKey = `level-${levelNumber}-completed`;
    if (levelCompleted === levelTotal && !progress[completionKey]) {
        progress[completionKey] = true;
        showModal(level);
    }
}

// Show completion modal
function showModal(level) {
    const modal = document.getElementById('congratsModal');
    const message = document.getElementById('modalMessage');
    message.textContent = `You've completed Level ${level.number}: ${level.title}! Ready for the next challenge?`;
    modal.classList.remove('hidden');
}

// Close modal
function closeModal() {
    document.getElementById('congratsModal').classList.add('hidden');
}

// Toggle all levels open/closed
function toggleAllLevels() {
    const levels = document.querySelectorAll('.level');
    const anyOpen = Array.from(levels).some(level => level.classList.contains('open'));
    
    levels.forEach(level => {
        if (anyOpen) {
            level.classList.remove('open');
        } else {
            level.classList.add('open');
        }
    });
}

// Export progress to JSON file
function exportProgress() {
    const data = {
        progress: progress,
        exported: new Date().toISOString(),
        stats: {
            totalItems: totalItems,
            completedItems: Object.keys(progress).filter(key => !key.includes('-completed')).length
        }
    };
    
    const blob = new Blob([JSON.stringify(data, null, 2)], { type: 'application/json' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = 'guitar-progress.json';
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(url);
}

// Reset all progress
function resetProgress() {
    if (confirm('Reset all progress? This cannot be undone.')) {
        progress = {};
        
        // Reset all visual states
        document.querySelectorAll('.checkbox').forEach(cb => cb.classList.remove('checked'));
        document.querySelectorAll('.topic-item').forEach(item => item.classList.remove('completed'));
        document.querySelectorAll('.level').forEach(level => level.classList.remove('completed'));
        
        updateAllProgress();
    }
}

// Initialize application
function init() {
    generateLevels();
    
    // Close modal on outside click
    window.onclick = function(event) {
        const modal = document.getElementById('congratsModal');
        if (event.target === modal) {
            closeModal();
        }
    };
    
    // Close modal on escape key
    document.addEventListener('keydown', function(event) {
        if (event.key === 'Escape') {
            closeModal();
        }
    });
}

// Start the application when DOM is loaded
document.addEventListener('DOMContentLoaded', init);

// Also start if DOM is already loaded
if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', init);
} else {
    init();
}
