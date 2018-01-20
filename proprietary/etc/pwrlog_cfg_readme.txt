/*
 * How to config powerlog configuration file
 * the configuration file supports four type parameters of sleeplogcat service: 
 * init/node/dumpsys/cmd
   * the file is limited less than 2k bytes
 */

!!!Warning: Don't insert any redundancy character (i.e. blank etc) in the pwrlog.cfg file!!!

[init]   		//max node quantity is 8
sleep_freq                 20        //capture dumpsys-log period is 20s
backup_folder_max_num      5        //powerlog backup max folder number;max_limit_value is 10*5
file_max_size	           5        //unit: Mbytes, max size of the wakelocks-log,to compress powerlog when log size is more than the threshold. max_limit_value is 10*5

[node]  //max node quantity is 32
{/proc/wakelocks,wakelocks-log    //the first parameters is node path, the second parameter is log info save name
/proc/interrupts,interrupt-log
/sys/kernel/debug/suspend_stats,suspendstats-log
/sys/kernel/debug/wakeup_sources,wakeupsources-log
/sys/kernel/debug/rpm_stats,rpm_stats-log
/sys/kernel/debug/rpm_master_stats,master_stats-log
/sys/kernel/debug/xo_voters,xo_voters-log
/sys/class/leds/lcd-backlight/brightness,brights-log 
//here to add it if you want to support more node
}

/*the first parameters is dumpsys parameter, the second parameter is dumpsys save name head */
[dumpsys]     //max node quantity is 32
{dumpsys alarm,alarm        
dumpsys cpuinfo,cpuinfo,
dumpsys batteryinfo,batinfo,
dumpsys usagestats,usestats,    
dumpsys telephony.registry,registry,
//here to add it if you want to support more dumpsys
}

/* need to execute command at the begin of start sleeplogcat service */
[cmd]     //max node quantity is 16
echo 1 > /sys/kernel/debug/clk/debug_suspend
/* 
 * here to add it if you want to support more cmd
 * be careful to use circulation command, i.e. top
 * correct usage:"top -n 5 -m 10" instead of "top" or "top -m 10"
 */
 }

 for example:
 
 [init]
5 5 1

[node]
{
/proc/wakelocks,wakelocks-log
/proc/interrupts,interrupt-log
/sys/kernel/debug/suspend_stats,suspendstats-log
/sys/kernel/debug/wakeup_sources,wakeupsources-log
/sys/kernel/debug/rpm_stats,rpm_stats-log
/sys/kernel/debug/rpm_master_stats,master_stats-log
/sys/kernel/debug/xo_voters,xo_voters-log
/sys/class/leds/lcd-backlight/brightness,brights-elog
}

[dumpsys]
{
dumpsys alarm,alarm
dumpsys cpuinfo,cpuinfo
dumpsys batteryinfo,batinfo
dumpsys usagestats,usestats
dumpsys telephony.registry,registry
}

[cmd]
{
echo 1 > /sys/kernel/debug/clk/debug_suspend
}



