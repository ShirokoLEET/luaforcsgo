--[[
    Hit log and fired log
    By Shiroko7
    Modify: Robonyantame (Bottame) xXYu3_zH3nGL1ngXx

    - Released on 17.09.2022 07:48
    - Beta 2.3
]]

--[[
    Changed logs:
    Release 2.3:
    - Improved code
    - Fixed miss log print in chat not working (wrong api but who know bottame do?)
        No. Chat custom color broken now :(
    - Many issues.
]]

-------------------------------------------

_DEBUG = true
--common.add_event("Hit", "check")
--common.add_event("Missed", "times")

-------------------------------------------

local GradientText = function(r1, g1, b1, a1, r2, g2, b2, a2, text)
    local output = ""
   local len = text:len() - 1
   local rinc = (r2 - r1) / len
   local ginc = (g2 - g1) / len
   local binc = (b2 - b1) / len
   local ainc = (a2 - a1) / len
   for i = 1, len + 1 do
       output = output .. ("\a%02x%02x%02x%02x%s"):format(r1, g1, b1, a1, text:sub(i, i))
       r1 = r1 + rinc
       g1 = g1 + ginc
       b1 = b1 + binc
       a1 = a1 + ainc
   end

   return output
end

local color_to_hex_text = function (color)
    return "\a" .. color:to_hex()
end

local hitgroups = {
    en = {
        [0] = "body",
        [1] = "head",
        [2] = "chest",
        [3] = "stomach",
        [4] = "left arm",
        [5] = "right arm",
        [6] = "left leg",
        [7] = "right leg",
        [8] = "neck",
        [9] = "generic",
        [10] = "unknown?"
    },
    cn = {
        [0] = "身子",
        [1] = "头部",
        [2] = "胸部",
        [3] = "肚子",
        [4] = "左手臂",
        [5] = "右手臂",
        [6] = "左腿",
        [7] = "右腿",
        [8] = "脖子",
        [9] = "整体",
        [10] = "未知"
    }
}

local reason_text = {
    en = {
        correction = {
            ["Default (correction)"] = "correction",
            ["Resolver"] = "Resolver",
            ["Unknown"] = "Unknown",
            ["?"] = "?",
        },
        misprediction = {
            --["Default (correction)"] = "correction misprediction",
            ["Default (correction)"] = "jitter misprediction",
            ["Resolver"] = "resolver misprediction",
            ["Unknown"] = "Unknown",
            ["?"] = "?",
        }
    },

    cn = {
        correction = {
            ["Default (correction)"] = "纠正",
            ["Resolver"] = "解析",
            ["Unknown"] = "未知",
            ["?"] = "?",
        },
        misprediction = {
            ["Default (correction)"] = "纠正误判",
            ["Resolver"] = "解析误判",
            ["Unknown"] = "未知",
            ["?"] = "?",
        }
    },

    misc_cn = {
        ["spread"] = "扩散",
        ["prediction error"] = "预判错误",
        ["death"] = "死亡",
        ["player death"] = "目标死亡",
        ["lagcomp failure"] = "回溯失效",
        ["unregistered shot"] = "未注册射击",
    }
}

-------------------------------------------

ui.sidebar(GradientText(146 ,254 ,157 ,255 ,0 ,201, 255,255,"Aimbot logger"), "user-tag")

local menu = {}

menu.gradient = {
    gamesense = "\ab7e810FFgamesense",
    neverlose = "\a4a69ffFFneverlose",
    advanced = GradientText(94 ,231 ,223,255,246,128,132,255,"Advanced"),
}

menu.combo = {
    fired_style = {menu.gradient.gamesense, menu.gradient.neverlose},
    langauge = {"English", "Chinese"},
    log_mode = {"Default", menu.gradient.advanced},
    resolver_output_mode = {"Default (correction)", "Resolver", "Unknown", "?"},
}

menu.handler = {
    fired                   = ui.create(GradientText(146 ,254 ,157 ,255 ,0 ,201, 255,255,"Ragebot fired logger")),
    logger                  = ui.create(GradientText(146 ,254 ,157 ,255 ,0 ,201, 255,255,"Aimbot logger")),
    notes                   = ui.create(GradientText(146 ,254 ,157 ,255 ,0 ,201, 255,255,"Notes and Contacts"))
}

menu.text = {
    text1                   = menu.handler.notes:label("Since the code of ver 2.3 is almost in a recoded but unstable state (other factors are that bottame doesn't know what some options do)"),
    text2                   = menu.handler.notes:label("Highlight miss reason color temporarily unavailable, Wait to improve"),
    text3                   = menu.handler.notes:label("If you encounter any code/script bug please contact us"),
    text4                   = menu.handler.notes:label("Owner: xXN1ckWa1k3rXx#8713\nModify: Robonyantame (Bottame)")
}


menu.fired = {
    switch                  = menu.handler.fired:switch(GradientText(146 ,254 ,157 ,255 ,0 ,201, 255,255,"Enabled ragebot fired logger")):set_tooltip("Enable ragebot's shooting log"),
    color_change_check      = menu.handler.fired:switch(GradientText(146 ,254 ,157 ,255 ,0 ,201, 255,255,"Custom Fired log color")),
    color_change            = menu.handler.fired:color_picker(GradientText(146 ,254 ,157 ,255 ,0 ,201, 255,255,"Fired log color"), color(255,255,255,255)),
    combo                   = menu.handler.fired:combo("\aF7FF8FFFlogger style", menu.combo.fired_style),
    langauge                = menu.handler.fired:combo("\aF7FF8FFFlogger language", menu.combo.langauge),
}


menu.logger = {
    switch                  = menu.handler.logger:switch(GradientText(146 ,254 ,157 ,255 ,0 ,201, 255,255,"Enabled aimbot logger")):set_tooltip("If enabled. the hit info and miss info will print on console."),
    top                     = menu.handler.logger:switch(GradientText(146 ,254 ,157 ,255 ,0 ,201, 255,255,"Enabled dev output")):set_tooltip("If enabled. the hit info and miss info will print on upper left corner of the screen \nIf you don't like it, you can turn it off. \nBut why??"),
    chat                    = menu.handler.logger:switch(GradientText(146 ,254 ,157 ,255 ,0 ,201, 255,255,"Print in Chat")),
    notify                  = menu.handler.logger:switch(GradientText(146 ,254 ,157 ,255 ,0 ,201, 255,255,"Enabled notify log")),
    notify_text             = menu.handler.logger:label("75%% Menu scale or 2k resolution is strongly recommended"),
    hit_color_change_check  = menu.handler.logger:switch (GradientText(146 ,254 ,157 ,255 ,0 ,201, 255,255,"Custom hit/miss log color")),
    hit_color_change        = menu.handler.logger:color_picker (GradientText(146 ,254 ,157 ,255 ,0 ,201, 255,255,"Hit log color"), color (255,255,255,255)),
    miss_color_change       = menu.handler.logger:color_picker (GradientText(146 ,254 ,157 ,255 ,0 ,201, 255,255,"Miss log color"), color (255,255,255,255)),
    hitloglist              = menu.handler.logger:combo(GradientText(146 ,254 ,157 ,255 ,0 ,201, 255,255,"Hitlog mode"), menu.combo.log_mode):set_tooltip("depends on your habit" .. "\nDefault: only show basic information" .. "\nAdvanced: show hc bc etc."),
    missloglist             = menu.handler.logger:combo(GradientText(146 ,254 ,157 ,255 ,0 ,201, 255,255,"Misslog mode"), menu.combo.log_mode):set_tooltip("show miss shot information \n\nTip: If you have the Ragebot fired logger enabled then Advanced is not necessary unless you want to look awesome"),
    misslist                = menu.handler.logger:combo("\aF7FF8FFFresolver output mode", menu.combo.resolver_output_mode):set_tooltip("\aFFFFFFFFThis is just an option to replace 'correction' in neverlose. \n\n\aF7FF8FFFwell known: correction = resolver\n\n\aFFFFFFFFSo if you don't like correction you can also replace it with resolver or unknown and ?\n\nThe premise is that you need to know that these are 'resolver issues'"),
    color                   = menu.handler.logger:switch("\aF7FF8FFFEnabled miss reason color"):set_tooltip("\a899facffIf enabled, use custom color miss reason in missed log output\n\n\ab7e810ffcorrection/resolver\n\af7ff8fffspread\n\a0097FFFFprediction error\n\a0097FFFFlagcomp failure\n\aC700FFFFunregistered shot\n\aFF0000FFplayer death/death"),
}


menu.setting = function ()

    menu.logger.top:set_visible(menu.logger.switch:get())
    menu.logger.chat:set_visible(menu.logger.switch:get())
    menu.logger.hit_color_change_check:set_visible(menu.logger.switch:get())
    menu.logger.hit_color_change:set_visible(menu.logger.switch:get() and menu.logger.hit_color_change_check:get())
    menu.logger.miss_color_change:set_visible(menu.logger.switch:get() and menu.logger.hit_color_change_check:get())
    menu.fired.color_change:set_visible(menu.fired.color_change_check:get())
    menu.logger.color:set_visible(false)
    -- menu.logger.chat:set_visible(false)

end

menu.logger.top:set(true)

-------------------------------------------

local callback = {

    ["render"] = function ()
        if ui.get_alpha() == 1 then
            menu.setting()
        end
    end,

    ["aim_fire"] = function (shot)
        
        if not menu.fired.switch:get() then return end

        local target = shot.target
        local target_name = target:get_name()

        -- neverlose bug
        if not shot or not target or target_name == "CWorld" or not target_name then return end

        local language_op = menu.fired.langauge:get()
        local style = menu.fired.combo:get()
        local fired_color = menu.fired.color_change:get()

        local table_lang = language_op == "English" and "en" or "cn"
        local hitboxes = language_op == "English" and hitgroups.en[shot.hitgroup] or hitgroups.cn[shot.hitgroup]
        local fired_hex = menu.fired.color_change_check:get() and color_to_hex_text(fired_color):sub(0 , 7) or "\aFFFFFF"
        local bodyyaw = math.floor(target.m_flPoseParameter[11] == nil and 0 or target.m_flPoseParameter[11] * 120 - 60) or "Unknown ?"
        

        local stylename = style == menu.gradient.gamesense and "\ab7e810[gamesense] " or "\a4a69ff[neverlose] "

        local data = {
            hitchance = math.floor(shot.hitchance),
            backtrack = shot.backtrack,
            damage = math.floor(shot.damage),
        }

        local text = {
            dev = {
                en = "Fired %s's %s Hitchance: %s Backtrack: %s tick Damage: %sHP body yaw: %s°",
                cn = "向 %s 的 %s  开枪射击 命中率: %s%% 回溯: %s tick  伤害: %sHP body yaw: %s°",
            },
            raw = {
                en = "%s%sFired %s's %s Hitchance: %s Backtrack: %s tick Damage: %sHP body yaw: %s°",
                cn = "%s%s向 %s 的 %s 开枪射击 命中率: %s%% 回溯: %s tick 伤害: %sHP body yaw: %s°",
            }
        }

       if menu.logger.top:get() == true then
        print_dev((text.dev[table_lang]):format(target_name, hitboxes, data.hitchance, data.backtrack, data.damage, bodyyaw))
       end

        print_raw((text.raw[table_lang]):format(stylename, fired_hex, target_name, hitboxes, data.hitchance, data.backtrack, data.damage, bodyyaw))

    end,

    ["aim_ack"] = function (shot)
        if not menu.logger.switch:get() then return end

        local target = shot.target
        local target_name = target:get_name()

        -- neverlose bug
        --if not shot or not target or target_name == "CWorld" or not target_name then return end

        if shot.target:is_bot() then
            target_name = "[Bot] " .. target_name
        end
        
        local language_op = menu.fired.langauge:get()
        local table_lang = language_op == "English" and "en" or "cn"
        local hitlogmode = menu.logger.hitloglist:get()
        local misslogmode = menu.logger.missloglist:get()
        local resolverlog = menu.logger.misslist:get()
        local chat_check = menu.logger.chat:get()
        local style = menu.fired.combo:get()
        local reasoncolor = menu.logger.color:get()
        local hit_color = menu.logger.hit_color_change:get()
        local miss_color = menu.logger.miss_color_change:get()
        
        local get_target_entity = entity.get(target)
        local hitboxes = language_op == "English" and hitgroups.en[shot.hitgroup] or hitgroups.cn[shot.hitgroup]
        local aimhb = language_op == "English" and hitgroups.en[shot.wanted_hitgroup] or hitgroups.cn[shot.wanted_hitgroup]
        local aimdmg = shot.wanted_damage

        local bodyyaw = math.floor(target.m_flPoseParameter[11] == nil and 0 or target.m_flPoseParameter[11] * 120 - 60) or "Unknown ?" -- unknown issues code


        local stylename = style == menu.gradient.gamesense and "\ab7e810[gamesense] " or "\a4a69ff[neverlose] "
        local hit_hex = menu.logger.hit_color_change_check:get() and color_to_hex_text(hit_color):sub(0, 7) or "\aFFFFFF"
        local miss_hex = menu.logger.hit_color_change_check:get() and color_to_hex_text(miss_color):sub(0, 7) or "\aFFFFFF"

        local color = {
            correction = reasoncolor and "\ab7e810" or miss_hex,
            misprediction = reasoncolor and "\ab7e810" or miss_hex,
            spread = reasoncolor and "\af7ff8f" or miss_hex,
            predictionerror = reasoncolor and "\a0097FF" or miss_hex,
            lcfailure = reasoncolor and "\a0097FF" or miss_hex,
            unregistered = reasoncolor and "\aC700FF" or miss_hex,
            death = reasoncolor and "\aFF0000" or miss_hex,
        }

        local data = {
            hitchance = math.floor(shot.hitchance),
            backtrack = shot.backtrack,
            damage = shot.damage ~= nil and math.floor(shot.damage) or 0,
            health = get_target_entity.m_iHealth,
        }
        

        if shot.state == nil then

            if chat_check then
                -- 颜色代码待修正
                local chat_style = style == menu.gradient.gamesense and "\4[gamesense]" or "\v[neverlose]"

                if chat_style == "\4[gamesense]" then
                    chat_en = "\a %s \1Hit \4%s \1the\4 %s\1 for\4 %s\1 damage (%s health remaining) with backtrack of \4%s\1 ticks"
                    chat_cn = "\a %s \1击中了 \4%s \1的\4 %s\1 造成\4 %s\1 的伤害 (剩余 %s 血) 和 \4%s\1 ticks回溯"
                end

                if chat_style == "\v[neverlose]" then
                    chat_en = "\a %s \1Hit \v%s \1the\v %s\1 for\v %s\1 damage (%s health remaining) with backtrack of \v%s\1 ticks "
                    chat_cn = "\a %s \1击中了 \v%s \1的\v %s\1 造成\v %s\1 的伤害 (剩余 %s 血) 和 \v%s\1 ticks回溯"
                end

                if language_op == "English" then
                    lang = chat_en
                elseif language_op == "Chinese" then
                    lang = chat_cn 
                end
                

                print_chat((lang):format(chat_style, target_name, hitboxes, data.damage, data.health, data.backtrack))
            end

            local text = {
                Default = {
                    dev = {
                        en = "Hit %s the %s for %s damage (%s health remaining) with backtrack of %s ticks",
                        cn = "击中了 %s 的 %s 造成了 %s 伤害 (剩余 %s 血) 和 %s ticks回溯",
                    },
                    raw = {
                        en = "%s%sHit %s the %s for %s damage (%s health remaining) with backtrack of %s ticks",
                        cn = "%s%s击中了 %s 的 %s 造成了 %s 伤害 (剩余 %s 血) 和 %s ticks回溯",
                    }
                },
                [menu.gradient.advanced] = {
                    dev = {
                        en = "Hit %s | Hitbox: %s | Hitchance: %s%% | Damage: %s HP (%s health remaining) | backtrack: %s tick | body yaw: %s°",
                        cn = "击中了 %s | 部位: %s | 命中率: %s% | 伤害: %s HP (剩余 %s 血) | 回溯: %s tick | body yaw: %s°",
                    },
                    raw = {
                        en = "%s%sHit %s | Hitbox: %s | Hitchance: %s%% | Damage: %s HP (%s health remaining) | backtrack: %s tick | body yaw: %s°",
                        cn = "%s%s击中了 %s | 部位: %s | 命中率: %s%% | 伤害: %s HP (剩余 %s 血) | 回溯: %s tick | body yaw: %s°",
                    } 
                },
            }

            if hitlogmode == "Default" then
                if menu.logger.top:get() == true then
                print_dev((text[hitlogmode]["dev"][table_lang]):format(target_name, hitboxes, data.damage, data.health, data.backtrack))
                end

                if menu.logger.notify:get() == true then
                    common.add_notify("Hit", ("Hit "..target_name.." the "..hitboxes.." for "..data.damage.." damage ("..data.health.." health remaining) with backtrack of ".. data.backtrack .." ticks"))
                end


                print_raw((text[hitlogmode]["raw"][table_lang]):format(stylename, hit_hex, target_name, hitboxes, data.damage, data.health, data.backtrack))
            elseif hitlogmode == menu.gradient.advanced then
                if menu.logger.top:get() == true then
                print_dev((text[hitlogmode]["dev"][table_lang]):format(target_name, hitboxes, data.hitchance, data.damage, data.health, data.backtrack, bodyyaw))
                end

                if menu.logger.notify:get() == true then
                    common.add_notify("Hit", ("Hit " .. target_name .. " | Hitbox: " .. hitboxes .. " | Hitchance: " .. data.hitchance .. "% | Damage: ".. data.damage .." HP (".. data.health .. " health remaining) | backtrack: "..data.backtrack.." tick | body yaw: " .. bodyyaw .."°"))
                end

                print_raw((text[hitlogmode]["raw"][table_lang]):format(stylename, hit_hex, target_name, hitboxes, data.hitchance, data.damage, data.health, data.backtrack, bodyyaw))
            end
            
            return
        end

        local state = ""
        local dev_state = ""

        if shot.state == "correction" or shot.state == "misprediction" then
            state = color[shot.state] .. reason_text[table_lang][shot.state][resolverlog]
            dev_state = reason_text[table_lang][shot.state][resolverlog]
        else
            local state_text = language_op == "English" and shot.state or reason_text.misc_cn[shot.state]
            state = (color[shot.state] or "\aFFFFFF") .. (state_text or "?")
            dev_state = state_text  or "?"
        end
    
        local miss_text = {
            Default = {
                dev = {
                    en = "Missed shot %s's %s due to %s",
                    cn = "空了 %s 的 %s 原因: %s",
                },
                raw = {
                    en = "%s%sMissed shot %s's %s due to %s",
                    cn = "%s%s空了 %s 的 %s 原因: %s",
                }
            },
            [menu.gradient.advanced] = {
                dev = {
                    en = "Missed shot %s | Reason: %s | Hitbox: %s | Damage: %sHP | Hitchance: %s | body yaw: %s°",
                    cn = "空了 %s | 原因: %s | 部位: %s | 预计伤害: %sHP | 命中率: %s | body yaw: %s°",
                },
                raw = {
                    en = "%s%sMissed shot %s | Reason: %s | Hitbox: %s | Damage: %sHP | Hitchance: %s | body yaw: %s°",
                    cn = "%s%s空了 %s | 原因: %s | 部位: %s | 预计伤害: %sHP | 命中率: %s | body yaw: %s°",
                } 
            },
        }

        if chat_check then

            -- 颜色代码待修正
            local chat_style = style == menu.gradient.gamesense and "\4[gamesense]" or  "\v[neverlose]"
            

            if chat_style == "\4[gamesense]" then
                miss_chat_en = "\a %s\1 Missed shot\4 %s\1's\4 %s\1 due to\4 %s"
                miss_chat_cn = "\a %s\1 空了\4 %s\1 的\4 %s\1 原因:\4 %s"
            end

            if chat_style == "\v[neverlose]" then
                miss_chat_en = "\a %s\1 Missed shot\v %s\1's\v %s\1 due to\v %s"
                miss_chat_cn = "\a %s\1 空了\v %s\1 的\v %s\1 原因:\v %s"
            end

            if language_op == "English" then
                miss_lang = miss_chat_en
            elseif language_op == "Chinese" then
                miss_lang = miss_chat_cn 
            end

            print_chat((miss_lang):format(chat_style, target_name, aimhb, dev_state))
        end

        if misslogmode == "Default" then
            if menu.logger.top:get() == true then
            print_dev((miss_text[misslogmode]["dev"][table_lang]):format(target_name, aimhb, dev_state))
            end
            print_raw((miss_text[misslogmode]["raw"][table_lang]):format(stylename, miss_hex, target_name, aimhb, state))

            if menu.logger.notify:get() == true then
                common.add_notify("Missed shot", ("Missed shot "..target_name.."'s "..aimhb.." due to "..dev_state..""))
            end

        elseif misslogmode == menu.gradient.advanced then
            if menu.logger.top:get() == true then
            print_dev((miss_text[misslogmode]["dev"][table_lang]):format(target_name, dev_state, aimhb, aimdmg, data.hitchance, bodyyaw))
            end
            print_raw((miss_text[misslogmode]["raw"][table_lang]):format(stylename, miss_hex, target_name, dev_state, aimhb, aimdmg, data.hitchance, bodyyaw))

            if menu.logger.notify:get() == true then
                common.add_notify("Missed shot", ("Missed shot "..target_name.." | Reason: "..dev_state.." | Hitbox: "..aimhb.." | Damage: "..aimdmg.."HP | Hitchance: ".. data.hitchance.." | body yaw: "..bodyyaw.."°"))
            end


        end
        
    end,

    ["player_hurt"] = function (e)

        local check = menu.logger.switch:get()
        if not check then return end

        local me = entity.get_local_player()
        if not me then return end

        local attacker = entity.get(e.attacker, true)
        if not attacker then return end
        
        local user = entity.get(e.userid, true)
        if not user then return end

        local local_player_name = me:get_name()
        local username = user:get_name()

        local language_op = menu.fired.langauge:get()
        local style = menu.fired.combo:get()

        local weapon = e.weapon
        local type_hit = 'Hit'
        local stylename = style == menu.gradient.gamesense and "\ab7e810[gamesense] " or "\a4a69ff[neverlose] "
        local table_lang = language_op == "English" and "en" or "cn"
    
        if weapon == 'hegrenade' then 
            type_hit = language_op == "English" and 'Naded' or '炸到了'
        end
    
        if weapon == 'inferno' then 
            type_hit = language_op == "English" and 'Burned' or '烧到了'
        end

        if weapon == 'knife' then 
            type_hit = language_op == "English" and 'Knifed' or '刀了'
        end
    
    
        if (weapon == 'hegrenade' or weapon == 'inferno' or weapon == 'knife') and me == attacker then

            local text = {
                raw = {
                    other = {
                        en = "%s%s %s for %s damage (%s health remaining)",
                        cn = "%s%s %s 造成了 %s 伤害 ( 剩余 %s 血)"
                    },
                    me = {
                        en = "%sYou are attacking yourself! (You only have %s health remaining)",
                        cn = "%s你在攻击你自己! (你只剩下 %s 的血量)"
                    }
                },
                dev = {
                    other = {
                        en = "%s %s for %s damage (%s health remaining)",
                        cn = "%s %s 造成了 %s 伤害 ( 剩余 %s 血)"
                    },
                    me = {
                        en = "You are attacking yourself! (You only have %s health remaining)",
                        cn = "你在攻击你自己! (你只剩下 %s 的血量)"
                    }
                }
            }

            if username ~= local_player_name then
                print_raw((text.raw.other[table_lang]):format(stylename, type_hit, username, e.dmg_health, e.health))

                if menu.logger.top:get() == true then
                print_dev((text.dev.other[table_lang]):format(type_hit, username, e.dmg_health, e.health))
                end


                
            elseif username == local_player_name then
                print_raw((text.raw.me[table_lang]):format(stylename, e.health))
                if menu.logger.top:get() == true then
                print_dev((text.dev.me[table_lang]):format(e.health))
                end


            end

        end
    end
}

for key, handle in pairs(callback) do
    events[key]:set(handle)
end
