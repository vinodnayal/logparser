elasticsearch-1.7.2
kibana-4.1.2
logstash-1.5.4

logstash conf file :

input {

  file {

    path => "/tmp/t4.log"

    type => "appl"

    codec => multiline {

        pattern => "^@"

        negate => true

        what => "previous"

    }

  }

}



filter {

  if [type] == "appl" {

    grok {

patterns_dir => "patterns"

        add_tag => [ "groked" ]

        match => ["message", "^@%{BCD_TIME:log_time}%{BCD}"]

 match => ["myatt", ".*"]

         remove_tag => ["_grokparsefailure"]

    }

  }

}





output {

  stdout { codec => rubydebug }

}





BCD .*


BCD_TIME ..:..:..

