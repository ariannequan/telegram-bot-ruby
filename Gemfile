source 'https://rubygems.org'
gem 'telegram-bot-ruby'
gem 'ip_info'

require 'rubygems'
require 'telegram/bot'
require 'ip_info'

token = '1264316235:AAERLlzs5xdzxHXnhuwmk_shLB1G41hzjvM'

@Ip_Add_ress_Bot = IpInfo::API.new(api_key: ENV["IP_INFO_KEY"])

Telegram::Bot::Client.run(token) do |bot|
  bot.listen do |message|
    case message.text
    when '/start'
      bot.api.send_message(chat_id: message.chat.id,
                          text: "Hello, #{message.from.first_name}")
    when /\/city [\w\W]+/
      bot.api.send_message(chat_id: message.chat.id,
                          text: get_info(get_address_form(message.text), 'city') )
    when /\/country [\w\W]+/
      bot.api.send_message(chat_id: message.chat.id,
                          text: get_info(get_address_form(message.text), 'country') )
    end
  end
end

def get_info(address, type)
  return 'Error: Address is invalid' unless address

  data = ''
  @ip_info.lookup(address, type: type).map do |e|
    data << e.first.to_s.gsub(/_/, ' ').capitalize + ': ' + e.last + "\n"
  end
  data
end
gemspec
