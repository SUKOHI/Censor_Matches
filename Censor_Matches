<?php

class Censor_Matches {

    private $_contents;
    private $_all_flag;
    private $_patterns;
    private $_places;

    public function __construct($contents, $all_flag=false) {

        $this->refresh();
        $this->_contents = $contents;
        $this->_all_flag = $all_flag;
        
    }

    public function setPatterns($patterns, $places) {

        if(!is_array($patterns)) {

            $patterns = array($patterns);

        }

        $this->_patterns = $patterns;
        $this->_places = $places;

    }

    public function getResult($cross_flag=false, $full_flag=true) {

        $return = array();
        $patterns = $this->_patterns;
        $patterns_count = count($patterns);

        for($loop = 0; $loop < $patterns_count; $loop++) {

            $pattern = $patterns[$loop];

            if($this->_all_flag) {

                $result = preg_match_all($pattern, $this->_contents, $matches);

            } else {

                $result = preg_match($pattern, $this->_contents, $matches);

            }

            if($result) {

                $places = $this->getPlaceCorrect($cross_flag, $loop);

                foreach($places as $key => $value) {

                    $match_value = $matches[$value];

                    if($match_value != '') {

                        $return[$key] = $matches[$value];

                    }

                }

                if(!$cross_flag) {

                    return $return;

                }

            } else if($cross_flag && $full_flag) {

                return false;

            }

        }

        return $return;

    }

    private function getPlaceCorrect($cross_flag, $loop) {

        if($cross_flag) {

            return $this->_places[$loop];

        } else {

            return $this->_places;

        }

    }

    public function refresh() {

        $this->_contents = $this->_all_flag = $this->_patterns = $this->_places = null;

    }

}

/*** Sample Source

    $patterns = '|(Regular Expression)|';   // String or Array
    $places = array('one' => 1, 'two' => 2);

    $cm = new Censor_Matches($contents);    // or use preg_match_all => $cm = new Simple_Matches($contents, true)
    $cm->setPatterns($patterns, $places);    // or get Cross => $cm->getResult(true); or get Cross Not Full $cm->getResult(true, false);
    $result = $cm->getResult();

***/
