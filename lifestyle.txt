!servalias lifestyle embed
<drac2>
args,n = &ARGS&,"\n"

if cc_exists("Experience"):
    None
else:
    Msg = f""" -desc 
    "
    Experience counter not setup.\nPlease type `!xp`
    "
    """
    return Msg
    
if exists("bags"):
    None
else:
    Msg = f""" -desc 
    "
    Coins not setup.\nPlease type `!coins`
    "
    """
    return Msg

one = get_cc("RPXP") if cc_exists("RPXP") else 0
two = get_cc("Jail") if cc_exists("Jail") else 0
three = get_cc("Staff") if cc_exists("Staff") else 0

create_cc("DT",0,5,"none","bubble")
create_cc("Jail",0,5,"none","bubble")
create_cc("Staff",0,50,"none")
create_cc("RPXP",0,proficiencyBonus*200,"none") 

set_cc("DT",5-two)
set_cc("Jail",0)
set_cc("Staff",0)
set_cc("RPXP",0)

staffe = three * 15 * proficiencyBonus

mod_cc("Experience",one+staffe)
days = get_cc("DT")

a = load_json(bags)
[a[x][1].update({"gp":a[x][1].gp-7}) for x in range(len(a)) if a[x][0] == 'Coin Pouch'][0]
set_cvar("bags",dump_json(a))
money = [a[x][1].get("gp") for x in range(len(a)) if a[x][0] == 'Coin Pouch'][0]

Msg=f""" -desc 
"
**Experience**
{"Staff Rewards: **" + str(staffe) + "xp**" + n if staffe > 0 else ""}{"RPXP: **" + str(one) + "xp**" + n if one > 0 else ""} Total: **{cc_str("Experience")}xp**

**Gold**
Modest lifestyle: **-7gp**
Total: **{money}gp**

**Counters**
{"Jail: **-" + str(two) + " DT**" + n if two > 0 else ""} Downtime: **{days} DT** 
"
"""

return Msg
</drac2>
-title "**<name>'s summary for the week!**"
-footer "Lifestyle | Summary | Peripéteia"
-thumb <image>
-color <color>
