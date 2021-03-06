# biometric-sync

PHP library for communicating with essl x990 biometric device via udp protocol

## Installation

```
composer require rajakannan/biosync
```
## Usage

```
<?php

require './vendor/autoload.php';

use Biosync\Biosync;

class Attendance {

    protected $ip;
    protected $device;
    /**
     * Create a new controller instance.
     *
     * @return void
     */
    public function __construct()
    {
        // set your essl attendance machine's IP here
        $this->ip = '192.168.1.7';
    }

    public function index()
    {
        $attendance = $this->getAttendance();
        var_dump($attendance);
    }

    public function connect()
    {
        $this->device = new Biosync($this->ip, 4370);
        $ret = $this->device->connect();
        $this->device->disableDevice();
    }

    public function disconnect()
    {
        $this->device->enableDevice();
        $this->device->disconnect();
    }

    public function getAttendance()
    {
        $this->connect();
        $attendance = $this->device->getAttendance();
        $this->disconnect();
        return $attendance;
    }
}
```