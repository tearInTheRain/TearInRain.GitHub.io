---
# the default layout is 'page'
icon: fas fa-info-circle
order: 4
---
<style>
  .weekly-summary {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    margin: 20px auto;
    padding: 1px 20px;
    background-color: #ffffff;
    box-shadow: 0 10px 30px rgba(0,0,0,0.1);
    border-radius: 8px;
  }
  .weekly-summary h2 {
    font-size: 24px;
    color: #333;
    margin-bottom: 20px;
    border-bottom: 2px solid #eee;
    padding-bottom: 10px;
  }
  .weekly-summary ul {
    list-style-type: none;
    padding-left: 0;
  }
  .weekly-summary li {
    margin-bottom: 8px;
    font-size: 16px;
    color: #555;
  }
   .goal-summary {
    display: grid;
    grid-template-columns: repeat(2, minmax(200px, 1fr)); /* 修改为每行展示2个项目 */
    gap: 15px;
    margin-top: 30px;
  }
  .goal-item {
    padding: 15px;
    background-color: #f8f9fa;
    border-radius: 6px;
    font-size: 16px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .goal-item.completed {
    background-color: #e8f5e9;
  }
  .emoji {
    font-size: 20px;
  }
  .total-goal {
    margin-top: 30px;
    margin-bottom: 15px;
    text-align: center;
    font-size: 18px;
    font-weight: bold;
    color: #333;
  }
</style>

<div class="weekly-summary">
  {% assign current_date = site.time | date: '%Y-%m-%d' %}
  {% assign week_start = current_date | date: '%Y-%m-%d' | date: '%s' | minus: 518400 | date: '%Y-%m-%d' %}
  {% assign a_count = 0 %}
  {% assign b_count = 0 %}
  {% assign c_count = 0 %}
  {% assign d_count = 0 %}
  
  <h2>本周博客</h2>
  <ul>
  {% for post in site.posts %}
    {% assign post_date = post.date | date: '%Y-%m-%d' %}
    {% if post_date >= week_start %}
      {% assign folder = post.path | split: '/' | slice: 1, 1 | first %}
      {% case folder %}
        {% when '编程' %}
          {% assign a_count = a_count | plus: 1 %}
        {% when '独立游戏' %}
          {% assign b_count = b_count | plus: 1 %}
        {% when '理财' %}
          {% assign c_count = c_count | plus: 1 %}
        {% when '摄影' %}
          {% assign d_count = d_count | plus: 1 %}
      {% endcase %}
      <li>{{ post.title }}</li>
    {% endif %}
  {% endfor %}
  </ul>
  
  <h2>本周目标</h2>
  <div class="goal-summary">
    <div class="goal-item {% if a_count >= 2 %}completed{% endif %}">
      <span>编程:{{ a_count }} / 2</span>
      <span class="emoji">{% if a_count >= 2 %}✅{% else %}🔲{% endif %}</span>
    </div>
    <div class="goal-item {% if b_count >= 1 %}completed{% endif %}">
      <span>独立游戏:{{ b_count }} / 1</span>
      <span class="emoji">{% if b_count >= 1 %}✅{% else %}🔲{% endif %}</span>
    </div>
    <div class="goal-item {% if c_count >= 1 %}completed{% endif %}">
      <span>理财:{{ c_count }} / 1</span>
      <span class="emoji">{% if c_count >= 1 %}✅{% else %}🔲{% endif %}</span>
    </div>
    <div class="goal-item {% if d_count >= 1 %}completed{% endif %}">
      <span>摄影:{{ d_count }} / 1</span>
      <span class="emoji">{% if d_count >= 1 %}✅{% else %}🔲{% endif %}</span>
    </div>
  </div>
  
    {% assign total_goal = false %}
    {% if a_count >= 2 and b_count >= 1 and c_count >= 1 and d_count >= 1 %}
    {% assign total_goal = true %}
    {% endif %}
  <div class="total-goal">
    {% if total_goal %}已达成 🎉{% else %}继续努力 💪{% endif %}
  </div>
</div>

<style>
  .monthly-summary {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    margin: 20px auto;
    padding: 1px 20px;
    background-color: #ffffff;
    box-shadow: 0 10px 30px rgba(0,0,0,0.1);
    border-radius: 8px;
  }
  .monthly-summary h2 {
    font-size: 24px;
    color: #333;
    margin-bottom: 20px;
    border-bottom: 2px solid #eee;
    padding-bottom: 10px;
  }
  .goal-summary {
    display: grid;
     grid-template-columns: repeat(2, minmax(200px, 1fr)); /* 修改为每行展示2个项目 */
    gap: 15px;
  }
  .goal-item {
    background-color: #f8f9fa;
    border-radius: 6px;
    padding: 15px;
    font-size: 16px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .goal-item.completed {
    background-color: #e8f5e9;
  }
  .goal-item.incomplete {
    background-color: #f8f9fa;
  }
  .emoji {
    font-size: 20px;
  }
  .tmp {
    margin-top: 30px;
    margin-bottom: 5px;
  }
</style>

<div class="monthly-summary">
  <h2>本月目标</h2>
  <div class="goal-summary">
    {% assign current_date = site.time | date: '%s' %}
    {% assign month_start = site.time | date: '%Y-%m-01' | date: '%s' %}
    
    {% assign a_count = 0 %}
    {% assign b_count = 0 %}
    {% assign c_count = 0 %}
    {% assign d_count = 0 %}
    
    {% for post in site.posts %}
      {% assign post_date = post.date | date: '%s' %}
      {% if post_date >= month_start and post_date <= current_date %}
        {% assign folder = post.path | split: '/' | slice: 1, 1 | first %}
        {% case folder %}
          {% when '编程' %}
            {% assign a_count = a_count | plus: 1 %}
          {% when '独立游戏' %}
            {% assign b_count = b_count | plus: 1 %}
          {% when '理财' %}
            {% assign c_count = c_count | plus: 1 %}
          {% when '摄影' %}
            {% assign d_count = d_count | plus: 1 %}
        {% endcase %}
      {% endif %}
    {% endfor %}
    
    <div class="goal-item {% if a_count >= 8 %}completed{% else %}incomplete{% endif %}">
      <span>编程:{{ a_count }} / 8</span>
      <span class="emoji">{% if a_count >= 8 %}✅{% else %}🔲 {% endif %}</span>
    </div>
    <div class="goal-item {% if b_count >= 4 %}completed{% else %}incomplete{% endif %}">
      <span>独立游戏:{{ b_count }} / 4</span>
      <span class="emoji">{% if b_count >= 4 %}✅{% else %}🔲{% endif %}</span>
    </div>
    <div class="goal-item {% if c_count >= 4 %}completed{% else %}incomplete{% endif %}">
      <span>理财:{{ c_count }} / 4</span>
      <span class="emoji">{% if c_count >= 4 %}✅{% else %}🔲{% endif %}</span>
    </div>
    <div class="goal-item {% if d_count >= 4 %}completed{% else %}incomplete{% endif %}">
      <span>摄影:{{ d_count }} / 4</span>
      <span class="emoji">{% if d_count >= 4 %}✅{% else %}🔲{% endif %}</span>
    </div>
    <div class="tmp">
    </div>
  </div>
</div>