---
layout: default
title: Newsletter
permalink: /newsletter/
---

<style>
    .newsletter-container { 
        max-width: 600px; 
        margin-top: 20px;
    }
    
    .timeline-hr { 
        border: none; 
        border-top: 1px solid #ddd; 
        margin: 1.5rem 0; 
    }

    .timeline-entry {
        border-left: 2px solid #ccc;
        padding: 0 0 1.5rem 1rem;
        position: relative;
    }
    
    .timeline-entry:last-child { 
        padding-bottom: 0; 
    }
    
    .timeline-dot {
        width: 8px; 
        height: 8px;
        border-radius: 50%;
        background: #aaa;
        position: absolute;
        left: -5px; 
        top: 6px;
    }
    
    .entry-date { 
        font-size: 11px; 
        color: #aaa; 
        margin-bottom: 4px; 
        font-family: monospace;
    }
    
    .entry-text { 
        font-size: 14px; 
        line-height: 1.6; 
        margin-top: 4px; 
    }

    .nl-tag {
        display: inline-block;
        font-size: 11px;
        padding: 2px 8px;
        border-radius: 4px;
        margin-bottom: 4px;
        font-family: monospace;
    }

    /* Your custom dynamic tag color map */
    .tag-Visits   { background: #dbeafe; color: #1e40af; }
    .tag-Updates    { background: #fef9c3; color: #854d0e; }
    .tag-Services  { background: #dcfce7; color: #166534; }
    .tag-Events  { background: #fce7f3; color: #9d174d; }
    .tag-Other     { background: #f1f5f9; color: #475569; }
</style>

<div class="newsletter-container">
    <h1>Newsletter</h1>
    <p style="font-size: 13px; color: #888;">Weekly home updates, logs, and events</p>
    <hr class="timeline-hr">
    
    <div id="entries">Loading timeline updates...</div>
</div>

<script>
document.addEventListener("DOMContentLoaded", function() {
    // Points directly to your simple clean JSON weekly asset
    const jsonUrl = "/pages/newsletter/26w24.json?nocache=" + Date.now();

    fetch(jsonUrl)
        .then(response => {
            if (!response.ok) {
                throw new Error("Could not find the target JSON file.");
            }
            return response.json();
        })
        .then(entries => {
            const div = document.getElementById('entries');
            if (!entries.length) {
                div.innerHTML = '<p style="color:#aaa;font-size:13px">No updates logged for this week.</p>';
                return;
            }
            
            // Maps your JSON keys ("date", "tag", "content") flawlessly into the timeline layout
            div.innerHTML = entries.map(e => `
                <div class="timeline-entry">
                    <div class="timeline-dot"></div>
                    <div class="entry-date">${e.date}</div>
                    <span class="nl-tag tag-${e.tag || 'Other'}">${e.tag}</span>
                    <p class="entry-text">${e.content}</p>
                </div>
            `).join('');
        })
        .catch(error => {
            console.error("Error building timeline asset context:", error);
            document.getElementById('entries').innerHTML = 
                '<p style="color:#aaa;font-size:13px">Failed to load this week\'s log updates.</p>';
        });
});
</script>