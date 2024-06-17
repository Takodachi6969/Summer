Bash scripts called by acron to sync data from the proANUBIS server to lxplus and cambridge. Currently have two different acron jobs:

scpProanub.sh is called every 15 minutes, and copies datafiles from the proANUBIS server to lxplus via rsync (despite the name...). It also uses the monitoring data to create a heatmap, which gets put into the monitoring directory and saved if it isn't identical to the last one. Lastly, it does a checksum of the most recent file on lxplus before and after copying files over. If they are identical, it sends out an email alert to the data shifters that no new data has been produced. When it sends an email, it sets a flag in the eos project space ("/eos/atlas/atlascerngroupdisk/proj-anubis/proANUBIS/data/monitor/emailTrigger.txt") that an email has been sent, and will not send another until the flag is reset.

backupCB.sh is called once every hour, and uses rsync to copy the data directory from lxplus to local storage at cambridge ("/r04/atlas/revering/data")