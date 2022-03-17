require './constants'
require 'json'

task :clean do
  sh "rm dst/*"
end

task :sequence do
  geojson = JSON.parse(`curl #{GEOJSON_URL}`)
  geojson['features'].each {|f|
    /src=\"(.*)\" /.match(f['properties']['画像'])
    url = $1.sub('/thumbnail', '')
    fn = %w{写真番号 name 撮影日時}.map{|k|
      f['properties'][k]
    }.join.gsub(':', '').gsub('-', '') + '.jpg'
    print "curl -o dst/#{fn} #{url}\n"
  }
end

task :download do
  sh <<-EOS
rake sequence | parallel -j #{J} {}
  EOS
end

