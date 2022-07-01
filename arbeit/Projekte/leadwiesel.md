# Technologie Stack
1. Laravel - https://laravel.com
	- composer https://getcomposer.org
2. Nuxt - https://nuxtjs.org
	- Vue - https://vuejs.org
	- Vuex - store - https://vuex.vuejs.org/guide
	- Vuetifyjs - https://nuxtjs.org/docs
	- axios - https://axios.nuxtjs.org/usage/


# SETUP
0. Git clone
	- datenbank - git clone "M:\WEB\Lead Wiesel\Umsetzung\lw2-container.git"
	- backend - git clone "M:\WEB\Lead Wiesel\Umsetzung\lw2-backend.git"
	- frontend - git clone "M:\WEB\Lead Wiesel\Umsetzung\lw2-frontend.git"



1. lw2-container, die Datenbank starten
	- der Ordner eintreten
	- docker-compose up
2. 


## DATA EINTRAGEN
Anruf
	- In der sales Tabelle muss ich next_call Spalte ändern. User_id, für die Eintrag, soll 313 sein.


## LARAVEL
apiResource - welche Endpunkte fugt apiResource hinzu
https://stackoverflow.com/questions/54721576/laravel-route-apiresource-difference-between-apiresource-and-resource-in-route



## NUXT
- nuxt 2.15.8 benutzt noch Vue 2 :/
- probleme mit Rerendering
	- Vue 2 macht kein Rerendering, wann Array oder Object wechseln sich, aber gibt es eine Lösung
	- https://michaelnthiessen.com/debugging-guide-why-your-component-isnt-updating/


## TODO

### Anrufliste
- Wenn man auf der Liste klickt, offnet es sich nicht mehr, nur Knopf [x]
- Zeitzone [x]
	- axios wechselt immmer die Zeit zu UTC, deswegen hat es 2 Stunden subtrahiert
	- https://www.php.net/manual/en/datetime.settimezone.php
	- Jetzt wechsle ich die Zeitzone in PHP
- Das ID von <v-expansion-panel> ist automatisch 0, 1, 2..., deswegen, wenn man mehr als ein expansion-panel hat, muss man mehr als ein v-model hat [x]
	- das :key macht keine Unterschied
	- habe ich ein Object erstellt 
		{
			"2019-06-03": [0, 1],
			"2020-01-14": [0]
		}





Arbeitzeit + 2h 40min