# Homework4

## Map-Reduce program

### Mapper
It picks the last five columns from the data which are relevant and creates <key,value> pairs with key value being lower cased column data and value being 1
Keys have been changed to upper case to standardise the result

### Reducer
It returns the sum of count of the keys after they the <key,value> pairs are sorted

## Commands for running the Map-Reduce program

Save the mapper and reducer file on the current directory

Give executable permissions to mapper and reducer class files
```
chmod +x reducer.py
chmod +x mapper.py 
```
To run the python files on local machine
```
cat /home/tatavag/nyc.data | python mapper.py | sort -k1,1 | python reducer.py
```

Here "nyc.data" is collected from the City of New York’s data website, and contains all reports of vehicular incidents in New York City over a period of time. The file is roughly 175MB in size, and contains over 900,000 records
It is uploaded on the hadoop cluster at the following HDFS location: /user/tatavag/nyc.data

### HDFS commands

To run Map-Reduce on Streaming API, the input and output files need to be on the HDFS. The input is already on the HDFS as stated above. 

The following command is used to run Map-Reduce program on HDFS
```
hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -file ./mapper.py -mapper ./mapper.py -file ./reducer.py -reducer ./reducer.py -input /tmp/nyc.data -output hw4_output
```

### Output log
```
jadhavsi@hadoop-gate-0:~$ hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -file ./mapper.py -mapper ./mapper.py -file ./reducer.py -reducer ./reducer.py -input /tmp/nyc.data -output hw4_output
19/04/22 23:15:51 WARN streaming.StreamJob: -file option is deprecated, please use generic option -files instead.
packageJobJar: [./mapper.py, ./reducer.py] [/usr/hdp/3.1.0.0-78/hadoop-mapreduce/hadoop-streaming-3.1.1.3.1.0.0-78.jar] /tmp/streamjob5342704419640850049.jar tmpDir=null
19/04/22 23:15:52 INFO client.RMProxy: Connecting to ResourceManager at hdfs-0-3.eecscluster/192.168.200.103:8050
19/04/22 23:15:52 INFO client.AHSProxy: Connecting to Application History server at hdfs-0-0.eecscluster/192.168.200.100:10200
19/04/22 23:15:52 INFO client.RMProxy: Connecting to ResourceManager at hdfs-0-3.eecscluster/192.168.200.103:8050
19/04/22 23:15:52 INFO client.AHSProxy: Connecting to Application History server at hdfs-0-0.eecscluster/192.168.200.100:10200
19/04/22 23:15:53 INFO mapreduce.JobResourceUploader: Disabling Erasure Coding for path: /user/jadhavsi/.staging/job_1549995810963_2253
19/04/22 23:15:53 INFO mapred.FileInputFormat: Total input files to process : 1
19/04/22 23:15:53 INFO mapreduce.JobSubmitter: number of splits:3
19/04/22 23:15:53 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1549995810963_2253
19/04/22 23:15:53 INFO mapreduce.JobSubmitter: Executing with tokens: []
19/04/22 23:15:54 INFO conf.Configuration: found resource resource-types.xml at file:/etc/hadoop/3.1.0.0-78/0/resource-types.xml
19/04/22 23:15:54 INFO impl.YarnClientImpl: Submitted application application_1549995810963_2253
19/04/22 23:15:54 INFO mapreduce.Job: The url to track the job: http://hdfs-0-3.eecscluster:8088/proxy/application_1549995810963_2253/
19/04/22 23:15:54 INFO mapreduce.Job: Running job: job_1549995810963_2253
19/04/22 23:16:03 INFO mapreduce.Job: Job job_1549995810963_2253 running in uber mode : false
19/04/22 23:16:03 INFO mapreduce.Job:  map 0% reduce 0%
19/04/22 23:16:13 INFO mapreduce.Job:  map 33% reduce 0%
19/04/22 23:16:14 INFO mapreduce.Job:  map 42% reduce 0%
19/04/22 23:16:17 INFO mapreduce.Job:  map 49% reduce 0%
19/04/22 23:16:18 INFO mapreduce.Job:  map 56% reduce 0%
19/04/22 23:16:20 INFO mapreduce.Job:  map 62% reduce 0%
19/04/22 23:16:21 INFO mapreduce.Job:  map 80% reduce 0%
19/04/22 23:16:24 INFO mapreduce.Job:  map 88% reduce 22%
19/04/22 23:16:26 INFO mapreduce.Job:  map 100% reduce 22%
19/04/22 23:16:30 INFO mapreduce.Job:  map 100% reduce 68%
19/04/22 23:16:33 INFO mapreduce.Job:  map 100% reduce 98%
19/04/22 23:16:34 INFO mapreduce.Job:  map 100% reduce 100%
19/04/22 23:21:36 INFO mapreduce.Job: Job job_1549995810963_2253 completed successfully
19/04/22 23:21:37 INFO mapreduce.Job: Counters: 54
        File System Counters
                FILE: Number of bytes read=65724275
                FILE: Number of bytes written=132393951
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=325141742
                HDFS: Number of bytes written=5161
                HDFS: Number of read operations=14
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=2
        Job Counters
                Launched map tasks=3
                Launched reduce tasks=1
                Data-local map tasks=2
                Rack-local map tasks=1
                Total time spent by all maps in occupied slots (ms)=225380
                Total time spent by all reduces in occupied slots (ms)=179880
                Total time spent by all map tasks (ms)=45076
                Total time spent by all reduce tasks (ms)=17988
                Total vcore-milliseconds taken by all map tasks=45076
                Total vcore-milliseconds taken by all reduce tasks=17988
                Total megabyte-milliseconds taken by all map tasks=230789120
                Total megabyte-milliseconds taken by all reduce tasks=184197120
        Map-Reduce Framework
                Map input records=1474746
                Map output records=2879784
                Map output bytes=59964701
                Map output materialized bytes=65724287
                Input split bytes=291
                Combine input records=0
                Combine output records=0
                Reduce input groups=605
                Reduce shuffle bytes=65724287
                Reduce input records=2879784
                Reduce output records=605
                Spilled Records=5759568
                Shuffled Maps =3
                Failed Shuffles=0
                Merged Map outputs=3
                GC time elapsed (ms)=5254
                CPU time spent (ms)=128730
                Physical memory (bytes) snapshot=5931094016
                Virtual memory (bytes) snapshot=29383204864
                Total committed heap usage (bytes)=5958008832
                Peak Map Physical memory (bytes)=2512723968
                Peak Map Virtual memory (bytes)=6250225664
                Peak Reduce Physical memory (bytes)=443772928
                Peak Reduce Virtual memory (bytes)=10738028544
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=325141451
        File Output Format Counters
                Bytes Written=5161
19/04/22 23:21:37 INFO streaming.StreamJob: Output directory: hw4_output
```

To display the output, use the following command-
```
hadoop fs -cat ./hw4_output/part-00000
```

### Map-Reduce Program Output
```
jadhavsi@hadoop-gate-0:~$ hadoop fs -cat ./hw4_output/part-00000
"       2
"red    1
"unk    1
(ceme   1
12 pa   3
15 pa   2
16m     1
18 wh   3
1s      1
2 doo   1
2 dr sedan      72
2 ton   1
2 whe   1
2- to   1
2ton    1
3 whe   1
3-door  112
3-whe   1
315 e   1
38ab-   1
3d      64
3dc-    1
4 dr sedan      1468
4 run   1
4d      2
4dr     1
4ds     3
4dsd    16
4whee   1
a       1
abula   1
acces   5
am      460
amabu   1
amb     21
ambu    32
ambul   442
ambulance       4790
amula   1
anbul   1
aport   1
appor   2
apurp   1
ar      81
armor   3
armored truck   145
army    1
axo     1
b5-44   1
ba      9
back    6
backh   18
bed     1
bed t   1
beverage truck  130
bicyc   2
bicycle 34109
bike    6418
bk      4
block   1
blue    1
boat    2
bob c   1
bobca   10
boom    6
booml   1
box     7
box t   51
box truck       11042
boxtr   2
br      70
broom   1
bs      2
bsd     2
bu      4297
bucke   3
budge   1
bulk agriculture        29
bulld   6
bus     34383
c-1     1
c0mme   1
c1      4
cab     1
cabin   1
camp    2
campe   1
car c   2
cargo   10
carri   3
carry all       772
cart    1
case    3
cat     5
cat 3   1
cat 4   1
cat 9   1
cat p   1
cate    1
cater   4
cb      174
cb534   1
cemen   4
chart   1
chassis cab     353
cherr   1
chevo   1
chevr   1
chevy   1
city    3
cm      106
cmix    4
cms-t   1
co      4
com     43
com t   3
com.    1
comb    1
comer   2
comix   1
comm    4
comme   57
commm   1
compa   1
concr   1
concrete mixer  242
const   15
cont    1
conta   1
conv    670
conve   1
convertible     1486
coupe   1
couri   3
crane   11
cushm   1
d       1
d1      1
del     1
deliv   62
delv    20
delv.   1
dema-   1
dept    1
detac   1
diese   2
dig-i   1
dirt    4
dirtb   2
dot #   1
dot r   1
dp      754
ds      2057
dsny    3
dump    1648
dumps   5
dumpt   2
dunba   1
e       1
e amb   2
e bik   7
e com   2
e one   1
e pas   1
e sco   3
e- bi   1
e-350   1
e-bik   20
e-mot   1
e.m.s   1
e/bik   1
e3      1
e350    1
east    1
eb      1
ebike   5
ec2     1
elec.   1
elect   73
emrgn   1
ems     2
ems a   2
ems b   2
ems h   1
en      2
enclosed body - nonremovable enclosure  1
enclosed body - removable enclosure     2
engin   2
epo     1
esu t   2
excav   6
expre   1
f550    1
farm    1
fb      478
fd fi   1
fd la   1
fd ny   1
fd tr   3
fdny    112
fed e   3
feder   1
fedex   2
fedx    1
fire    156
fire truck      1507
firet   45
flat    22
flat bed        992
flat rack       157
flatb   10
fleet   1
fltrl   1
food    9
foor    1
ford    15
fork    33
fork-   1
forkl   77
fortl   1
fr      61
fr`     1
fre     1
fre t   1
free    1
freig   25
frht    2
frieg   4
front   3
g com   3
g omr   1
g pas   1
g sem   1
g tow   1
g1`     1
garab   1
garba   31
garbage or refuse       953
gas s   1
gas t   1
gator   3
ge/sc   1
geico   1
gg      403
glass rack      6
glben   1
gmc v   1
gn      1
gokar   1
golf    10
gov v   2
gov't   1
gover   6
gr      3
grain   3
gray    2
h/wh    1
hand    2
harve   1
heavy   1
help    1
hi-lo   2
highl   1
hino    6
ho      3
hoe-l   1
hook    1
hopper  8
horse   4
hotdo   1
house   1
hrse    1
humme   1
hwy c   1
ice c   3
icecr   1
inter   4
ip      1
jcb40   1
jeep    3
jlg b   1
john    2
johnd   2
ken     1
kenwo   2
ladde   1
large com veh(6 or more tires)  29008
ld      1
lf      30
lg      1
liber   1
lift    2
lift boom       81
light   6
limo    4
limo/   1
limou   6
liver   2
livery vehicle  19419
livestock rack  10
ll      345
loade   1
log     3
lp      1
ltrl    1
lunch wagon     15
lw      6
mac t   1
mack    11
mail    13
man l   2
mark    1
marke   1
maxim   1
mb      45
mc      1
mcy     1
mcy b   1
md      69
me/be   1
mecha   2
metal   1
mh      5
milli   1
mini    7
minibike        12
minicycle       11
miniv   2
mk      5
mo pa   1
mopad   2
mopd    2
moped   240
mopet   2
mot s   1
moter   1
motor   39
motor home      1
motorbike       136
motorcycle      15183
motorized home  13
motorscooter    232
movin   2
ms      78
mta     1
mta b   18
mta c   1
mta t   1
mtr s   1
multi-wheeled vehicle   39
mv      2
n/a     6
na      2
nd      1
new y   4
nissa   2
none    1
ns am   1
nv150   1
nyc     1
nyc a   2
nyc b   1
nyc d   2
nyc f   5
nyc m   1
nycha   1
nypd    6
objec   1
off r   1
oil t   4
olc     1
olm     1
oml     2
oml/    1
omni    1
omnib   6
omr     12
omt     5
op      6
open body       30
other   51089
p/se    1
p/sh    12
palle   1
pallet  17
pas     30
pass    2
passa   1
passe   4
passenger vehicle       1341743
pavin   1
paylo   2
pc      5
pch     1
pedic   3
pedicab 195
pick    23
pick-   9
pick-up truck   61083
picku   19
pickup with mounted camper      21
pish    1
pk      1243
pkup    1
pl      9
plow    1
pm      10
pois    1
porta   1
post    1
posta   31
posto   1
power   30
psd     7
psr     1
pu      1
pump    1
pumpe   1
push    1
r/v     2
r/v c   1
ram     1
rd/s    3
red t   2
refg    9
refri   3
refrigerated van        202
renta   3
rep     3
repai   1
rescu   3
rf      127
rgs     1
rmb     1
rmp     3
rmp v   1
road    4
roads   1
rubbe   1
rv      23
rv/tr   1
ryder   1
s/sp    1
safet   1
sanit   30
santa   1
sbn     1
sc      2
scaff   1
scava   1
schoo   72
school bus      47
sciss   2
scl     1
scoo    1
scoot   55
scooter 573
se      2
sea     1
seagr   1
sedan   178300
segwa   1
self    20
self-   1
semi    12
semi-   9
sgws    1
shcoo   1
skate   4
skid    1
small   2
small com veh(4 tires)  4
small com veh(4 tires)  30972
smart   2
snow    2
snow plow       30
sp      34
spc     8
spc p   1
spec    1
sport utility / station wagon   599137
sprin   10
ss      1
st      27
st150   1
stak    7
stake or rack   57
state   1
station wagon/sport utility vehicle     143272
stree   27
sub     2
subn    14
subn/   1
subur   6
sudan   1
suv     6
sw      2
sweep   4
swt     1
sybn    1
tan p   1
tandu   1
tank    12
tanke   3
tanker  347
taxi    116636
tcn     1
te      1
tf      1
tk      5329
tl tr   1
tlr     2
tn      162
tour    1
tow     20
tow t   56
tow truck       13
tow truck / wrecker     510
tow-t   1
tower   2
towtr   2
tr      339
tr/ki   1
trac    17
trac.   1
track   8
tract   85
tractor truck diesel    4730
tractor truck gasoline  690
traff   1
trail   247
train   1
tram    1
trans   4
trash   1
trial   2
trk     10
trl     14
trlpm   1
trlr    5
trt     1
truck   190
tt      237
u-hau   6
u.s p   1
u.s.    1
uber    1
ud      1
uhaul   8
uhual   1
ukn     1
ulili   1
uliti   1
unk     38
unkn    1
unkno   87
unknown 105289
unkow   3
unnko   1
ups t   4
us ma   1
us po   15
uspos   2
usps    64
usps2   1
uspst   1
ut      1
util    18
utili   41
utlit   1
utll    1
utv     1
vab     1
van     56636
van a   1
van c   2
van camper      13
van f   1
van t   12
van w   1
van/b   1
van/t   4
van`    1
vanette 6
vang    1
vav     1
vc      9
veriz   2
vn      1390
vol     1
vt      4
wagon   7
waste   1
wc      1
wd      2
well driller    7
wesco   1
whbl    1
wheel   2
white   14
winne   2
work    5
workh   1
yello   10
omm     1
```




