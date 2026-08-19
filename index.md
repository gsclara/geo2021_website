---
layout: default
title: Home
---

# Modeling wind and dispersion 

<div class="container">
	<div class="row">
		<div class="col-md-12">
			<div class="alert alert-success" role="alert">
				<i class='fas fa-map-marked-alt'></i> Classes are mostly in BK Room Z, but please check the schedule. Friday's help session is in the Geolab (BG.Oost.620).
			</div>
		</div>
		<div class="col-md-3">
			<div class="card bg-light border-light">
			  <div class="card-body">
			    <h5 class="card-title">recent news</h5>
			    {% assign sorted = site.data.news | sort: 'date' | reverse %}
			    {% for news in sorted limit:5 %}
			      <p><span class="badge">{{ news.date | date: "%b %d" }}</span> {{ news.news | markdownify | remove: '<p>' | remove: '</p>' }}</p>
			    {% endfor %}
			    <a href="{{ site.baseurl }}/news/">all news</a>
			  </div>
			</div>
			<br />
		</div>
		<div class="col-md-9">
			<div class="table-responsive">
				<table class="table table-hover">
				  <thead class="table-light">
				    <tr>
				      <th scope="col">week</th>
				      <th scope="col">{{ site.period1 }}</th>
				      <th scope="col">{{ site.period2 }}</th>
				      <th scope="col">{{ site.help }}</th>
				      <th scope="col">other to dos</th>
				    </tr>
				  </thead>
				  <tbody>
				  	{% assign startweek = site.start | date: "%s" | plus: 0 %}
				  	{% for week in (1..10) %}
				  		{% assign endweek = startweek | date: "%s" | plus: 345600 %}
				  		{% assign startweekdate = startweek | date: "%b&nbsp;%d" %}
				  		{% assign endweekdate = endweek | date: "%b&nbsp;%d" %}
				  		{% for w in site.data.weeks %}
				  			{% if w.week == week %}
						  		{% assign l1 = w.lesson1 %}
						  		{% assign l2 = w.lesson2 %}
						  		{% assign todos = w.todos | split: ", " %}
						  		{% assign submit = w.submit %}
						  		{% assign continue = w.continue %}
						  		{% assign start = w.start %}
						  		{% assign help = w.help %}
						  		{% assign room1 = w.room1 %}
						  		{% assign room2 = w.room2 %}
						  		{% assign roomhelp = w.roomhelp %}
				  			{% endif %}
		  				{% endfor %}
		  				{% if submit %}
		  					{% assign hwarray = submit | split: "_" %}
		  					{% for hw in site.data.homework %}
	  							{% assign hwn = hwarray[1] | plus: 0 %}
	  							{% if hw.number == hwn %}
	  								{% if hw.deadline %}
		  								{% assign deadline = hw.deadline | date: "%b %d" %}
	  								{% endif %}
	  							{% endif %}
	  						{% endfor %}
		  				{% endif %}
		  				{% assign lesson1 = nil %}
		  				{% assign lesson2 = nil %}
		  				{% for l in site.data.lessons %}
		  					{% if l.lesson == l1 %}
		  						{% assign lesson1 = l %}
		  					{% endif %}
		  					{% if l.lesson == l2 %}
		  						{% assign lesson2 = l %}
		  					{% endif %}
		  				{% endfor %}
				  		<tr>
				  			<th scope="row">{{ site.quarter }}.{{ week }}<br /><small class="fw-normal">{{ startweekdate }}&nbsp;-&nbsp;{{ endweekdate }}</small></th>
			  				<td>
			  					{% if lesson1 %}
			  						{% if lesson1.publish %}
			  							<a href="les/{{ l1 }}"><i class="fas fa-book-reader"></i> lesson {{ week }}.1 ({{ l1 }})</a>
			  						{% else %}
			  							<i class="fas fa-book-reader"></i> lesson {{ week }}.1 ({{ l1 }})
			  						{% endif %}
		  							{% if lesson1.live %}
		  								<br />{{ lesson1.live }}
			  						{% endif %}
			  						{% if room1 %}
			  							<br /><i class='fas fa-map-marked-alt'></i> {{ room1 }}
			  						{% endif %}
		  						{% endif %}
			  				</td>
			  				<td>
			  					{% if lesson2 %}
			  						{% if lesson2.publish %}
			  							<a href="les/{{ l2 }}"><i class="fas fa-book-reader"></i> lesson {{ week }}.2 ({{ l2 }})</a>
			  						{% else %}
			  							<i class="fas fa-book-reader"></i> lesson {{ week }}.2 ({{ l2 }})
			  						{% endif %}
		  							{% if lesson2.live %}
		  								<br />{{ lesson2.live }}
			  						{% endif %}
			  						{% if room2 %}
			  							<br /><i class='fas fa-map-marked-alt'></i> {{ room2 }}
			  						{% endif %}
		  						{% endif %}
			  				</td>
			  				<td>
			  					{% if help == true %}
				  					help session
				  					{% if roomhelp %}
				  						<br /><i class='fas fa-map-marked-alt'></i> {{ roomhelp }}
				  					{% endif %}
				  				{% endif %}
			  				</td>
					  		<td>
			  					{% if submit %}
			  						{% assign hwarray = submit | split: "_" %}
			  						{% assign newtodo = '<strong>submit <a href="hw/' | append: hwarray[1] | append: '">homework ' | append: hwarray[1] | append: '</a>' %}
	  								{% if deadline %}
		  								{% assign newtodo = newtodo | append: ' (' | append: deadline | append: ')' %}
	  								{% endif %}
			  						{% assign newtodo = newtodo | append: '</strong>' %}
			  						{% assign todos = todos | push: newtodo %}
			  					{% endif %}
			  					{% if continue %}
			  						{% assign hwarray = continue | split: "_" %}
			  						{% assign newtodo = 'continue <a href="hw/' | append: hwarray[1] | append: '">homework ' | append: hwarray[1] | append: '</a>' %}
			  						{% assign todos = todos | push: newtodo %}
			  					{% endif %}
			  					{% if start %}
			  						{% assign hwarray = start | split: "_" %}
			  						{% assign newtodo = 'start <a href="hw/' | append: hwarray[1] | append: '">homework ' | append: hwarray[1] | append: '</a>' %}
			  						{% assign todos = todos | push: newtodo %}
			  					{% endif %}
			  					{{ todos | join: ', ' }}
				  			</td>
				  		</tr>
				  		{% assign startweek = startweek | date: "%s" | plus: 604800 %}
				  	{% endfor %}
				  	<tr>
				  		<th scope="row">2.3 <br /><small class="fw-normal">Nov&nbsp;23&nbsp;-&nbsp;Nov&nbsp;27</small></th>
				  		<td></td>
			  			<td></td>
			  			<td></td>
			  			<td>
			  				resits for <strong><a href="hw/resit/">assignments</a></strong> ({{ site.resit | date: "%b&nbsp;%d&nbsp;@&nbsp;%H:%M" }})<br />
			  				tbd</td>
				  	</tr>
				  </tbody>
				</table>
			</div>
		</div>
	</div>
</div>
