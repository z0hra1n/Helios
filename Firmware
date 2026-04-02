from gpiozero import AngularServo
from skyfield.api import load, Topos
import time

az = AngularServo(18)
el = AngularServo(19)

lat = 19.0760
lon = 72.8777

ts = load.timescale()
satellites = load.tle_file('https://celestrak.org/NORAD/elements/noaa.txt')

sat = [s for s in satellites if 'NOAA 19' in s.name][0]
observer = Topos(latitude_degrees=lat, longitude_degrees=lon)

while True:
t = ts.now()
alt, azm, _ = (sat - observer).at(t).altaz()

azimuth = azm.degrees  
elevation = alt.degrees  

if elevation > 0:  
    az.angle = azimuth / 2  
    el.angle = elevation  

time.sleep(1)
