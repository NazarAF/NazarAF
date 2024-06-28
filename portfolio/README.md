# 📋 Portfolio Project

<!-- Experience 1 -->
## Desa Sumber Sari (January 2023 - February 2023)
### 📄 Description
This website is my first job as a freelancer and as a full stack developer, in this website I was assigned to create a website for publication in Sumber Sari, the features available on this website are news, agenda, gallery, complaints, and reservations, here is the list the work I do on this website:
- Creating backend with Laravel.
- Creating frontend with Javascript & JQuery.
- Creating database.
- Creating unit and feature test.
- Hosting application.
### 💻 Tech Stack
![PHP](https://img.shields.io/badge/php-%23777BB4.svg?style=for-the-badge&logo=php&logoColor=white) ![Laravel](https://img.shields.io/badge/laravel-%23FF2D20.svg?style=for-the-badge&logo=laravel&logoColor=white) ![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E) ![Apache](https://img.shields.io/badge/apache-%23D42029.svg?style=for-the-badge&logo=apache&logoColor=white) ![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=orange)
<!-- Experience 1 -->

<!-- Experience 2 -->
## RT. 08 Sempaja Utara (March 2023 - June 2023)
### 📄 Description
On this website I was assigned to create an information system for government agencies, the features I created on this website were population data collection, scheduling meetings or agendas, writing letters, and validating emails for accounts registered in the application. Below is a list of work I do on this website:
- Creating backend with Laravel.
- Creating frontend with Javascript & JQuery.
- Creating and Design database.
- Documentary application.
### 💻 Tech Stack
![PHP](https://img.shields.io/badge/php-%23777BB4.svg?style=for-the-badge&logo=php&logoColor=white) ![Laravel](https://img.shields.io/badge/laravel-%23FF2D20.svg?style=for-the-badge&logo=laravel&logoColor=white) ![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E) ![Apache](https://img.shields.io/badge/apache-%23D42029.svg?style=for-the-badge&logo=apache&logoColor=white) ![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=orange)
<!-- Experience 2 -->

<!-- Experience 3 -->
## Sistem Informasi Sebaran Penyakit Hewan (June 2023 - July 2023)
### 📄 Description
This website is the first work with a team and remotely. This website was submitted by the government to collect data on animal diseases and their spread using geolocation. On this website, my tasks include improving website optimization, creating geolocation, improving the frontend. The following is a list of work I do on this website:
- Updating feature backend with Laravel.
- Updating frontend with Javascript & JQuery.
- Remoting with Git and SFTP.
### 💻 Tech Stack
![PHP](https://img.shields.io/badge/php-%23777BB4.svg?style=for-the-badge&logo=php&logoColor=white) ![Laravel](https://img.shields.io/badge/laravel-%23FF2D20.svg?style=for-the-badge&logo=laravel&logoColor=white) ![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E) ![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white) ![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=orange)
<!-- Experience 3 -->

<!-- Experience 4 -->
## Medisin - PT Sintesa Persada Teknologi (June 2023 - Now)
### 📄 Description
This website is a hospital service website, PT Sintesa is a vendor for several hospitals in Indonesia, my task on this website is to create new features such as patient letters, recording costs and cost recapitulation, recording patient visits, and recording patient diagnoses, the following are list of work I do on this website:
- Creating & Update feature backend with Laravel.
- Creating & Update feature frontend with Vue.js
- Remoting with Git and SFTP.
### 💻 Tech Stack
![PHP](https://img.shields.io/badge/php-%23777BB4.svg?style=for-the-badge&logo=php&logoColor=white) ![Laravel](https://img.shields.io/badge/laravel-%23FF2D20.svg?style=for-the-badge&logo=laravel&logoColor=white) ![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E) ![Vue.js](https://img.shields.io/badge/vuejs-%2335495e.svg?style=for-the-badge&logo=vuedotjs&logoColor=%234FC08D) ![NodeJS](https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white) ![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white) ![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white)
<!-- Experience 4 -->

# 📱 Sample Code
Because all the projects I work on are personal projects, I created this section to illustrate how I write code by providing a little code from the projects I have worked on above.
<details>
<summary>Authentication with Custom OTP and Email Verification</summary>

Setup Method in User Model
```php
private function mail(array $message) {
    return $response = (new \GuzzleHttp\Client())->post(env('MAIL_HOST'), [
        'headers' => [
            'Authorization' => 'Bearer ' . env('MAIL_TOKEN'),
            'Content-Type'  => 'application/json'
        ],
        'body' => json_encode($message),
    ]);
}

public function verify() {
    $message = [
        "from"                  => [
            "email" => env('MAIL_FROM_ADDRESS'),
            "name"  => "Email Verification"
        ],
        "to"                    => [["email" => $this->email]],
        "template_uuid"         => env('MAIL_EMAIL_VERIFICATION_TEMPLATE'),
        "template_variables"    => [
            "app_name"          => env('APP_NAME'),
            "user_email"        => $this->email,
            "pass_reset_link"   => (new VerifyEmail())->toMail($this)->actionUrl,
        ]
    ];

    return json_decode($this->mail($message)->getBody())->success;
}

public function reset() {
    $otp = Otp::setValidity(30)->setLength(6)->setOnlyDigits(true)->setUseSameToken(false)->generate($this->email);

    $message = [
        "from"                  => [
            "email" => env('MAIL_FROM_ADDRESS'),
            "name"  => "Reset Password"
        ],
        "to"                    => [["email" => $this->email]],
        "template_uuid"         => env('MAIL_OTP_TEMPLATE'),
        "template_variables"    => [
            "app_name"      => env('APP_NAME'),
            "user_email"    => $this->email,
            "otp"           => $otp->token
        ]
    ];

    return json_decode($this->mail($message)->getBody())->success;
}

public function deleteToken() {
    $this->token()->delete();
    return $this;
}
```

How to use verification email
```php
public function resend() {
    try {
        auth()->user()->verify();
        return back()->with('resent', true);
    } catch(Exception $e) {
        return back()->with('resent', false);
    }
}
```

How to use OTP
```php
public function sendOTP(Request $request) {
    if (!(Validator::make($request->all(), ['email' => 'required|email']))->fails())
        if ($user = User::where('email', '=', $request->email)->first()) {
            $user->reset();
            return redirect()->route('password.validate', ['email' => $request->email]);
        }

    return back()->with('resent', true);
}

public function validateToken(Request $request) {
    if (!(Validator::make($request->all(), ['email' => 'required|email', 'otp' => 'required']))->fails())
        if ($token = Token::where('identifier', $request->email)->where('token', $request->otp)->where('expired', false)->first()) {
            if (Carbon::parse(Carbon::now())->diffInMinutes(Carbon::parse($token->updated_at)) > $token->validity) {
                $token->update(['expired' => true]);
                return back()->with('resent', true);
            }

            return view('auth.passwords.reset', ['email' => $request->email, 'otp' => $request->otp]);
        }

    return back()->with('resent', true);
}

public function reset(Request $request) {
    if (!(Validator::make($request->all(), ['email' => 'required|email', 'otp' => 'required', 'password' => 'required|confirmed']))->fails())
        if ($token = Token::where('identifier', $request->email)->where('token', $request->otp)->where('expired', false)->first()) {
            if (Carbon::parse(Carbon::now())->diffInMinutes(Carbon::parse($token->updated_at)) > $token->validity) {
                $token->update(['expired' => true]);
                return back()->with('resent', true);
            }

            User::where('email', '=', $request->email)->first()->deleteToken()->update(['password' => bcrypt($request->password)]);
            return redirect()->route('login');
        }

    return back()->with('resent', true);
}
```
</details>

<details>
<summary>Build Controller</summary>

How do I usually create a controller, with this structure, I can easily create validation for each controller.
```php
<?php

namespace App\Http\Controllers\Admin;

// Library
use App\Http\Controllers\Controller;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Validator;
use Maatwebsite\Excel\Excel as Excels;
use Maatwebsite\Excel\Facades\Excel;
use Carbon\Carbon;
use DataTables;
use File;

// Extension
use App\Helpers\Crypt;

// Credentials Controller
use App\Models\User;
use App\Models\Family;
use App\Exports\UsersExport;
use App\Imports\UsersImport;

class UsersController extends Controller
{
    /*
    |--------------------------------------------------------------------------
    | Users Controller
    |--------------------------------------------------------------------------
    |
    | This controller handles view all users
    | insert, update, delete, import, and export users.
    |
    */

    /**
     * Display a listing of the resource.
     *
     * @param  \Illuminate\Http\Request $request
     * @return \Illuminate\Http\Response
     */
    public function index(Request $request)
    {
        if ($request->ajax())
            return Datatables::of(User::search($request->search)->filters($request->filters)->get(['id_user', 'id_family', 'username', 'email', 'role']))
                    ->addIndexColumn()
                    ->addColumn('kk', function($user){
                        if($user->id_family)
                            return "<button class='btn btn-info' onClick='family(" . $user->id_family . ")'>
                                        <i class='fas far fa-newspaper'></i>
                                    </button>";
                        else
                            return "<span class='badge badge-danger font-weight-bold'>None</span>";
                    })
                    ->addColumn('role', function($user){
                        if($user->role)
                            return "<span class='badge badge-primary font-weight-bold'>Admin</span>";
                        else
                            return "<span class='badge badge-info font-weight-bold'>User</span>";
                    })
                    ->addColumn('action', function($user){
                        return  "<button class='btn btn-warning my-2' onClick='edit($user->id_user)'>
                                    <i class='fas fa-edit'></i>
                                </button>
                                <button class='btn btn-danger my-2' onClick='destroy($user->id_user)'>
                                    <i class='fas fa-trash-alt'></i>
                                </button>";
                    })
                    ->rawColumns(['action', 'role', 'kk'])
                    ->toJson();

        return view('admin.users');
    }

    /**
     * Store a newly created resource in storage.
     *
     * @param  \Illuminate\Http\Request $request
     * @return \Illuminate\Http\Response
     */
    public function store(Request $request)
    {
        if (!$this->validation($request->all()))
            return response([
                'title'     => 'Failed!',
                'message'   => 'Add User',
                'type'      => 'error'
            ], 200);

        User::create([
            'id_family'         => $request->id_family,
            'email'             => $request->email,
            'phone'             => $request->phone,
            'username'          => $request->username,
            'role'              => $request->role,
            'password'          => bcrypt($request->password),
            'email_verified_at' => $request->email_verified_at,
        ]);

        return response([
            'title'     => 'Success!',
            'message'   => 'Add User',
            'type'      => 'success'
        ], 200);
    }

    /**
     * Show the data for editing the specified resource.
     *
     * @param  App\Models\User $user
     * @return \Illuminate\Http\Response
     */
    public function edit(User $user)
    {
        if ($user) {
            return response()->json($user, 200);
        } else {
            return response([
                'title'     => 'Failed!',
                'message'   => 'Edit User',
                'type'      => 'error'
            ], 400);
        }
    }

    /**
     * Update the specified resource in storage.
     *
     * @param \App\Models\User $user
     * @param \Illuminate\Http\Request $request
     * @return \Illuminate\Http\RedirectResponse
     */
    public function update(Request $request, User $user)
    {
        if (!$this->validation($request->all(), $user, true))
            return response([
                'title'     => 'Failed!',
                'message'   => 'Update User',
                'type'      => 'error'
            ], 200);

        $user->update([
            'id_family'         => $request->id_family,
            'email'             => $request->email,
            'phone'             => $request->phone,
            'username'          => $request->username,
            'role'              => $request->role,
            'password'          => $request->password ? bcrypt($request->password) : $user->password,
            'email_verified_at' => $request->email_verified_at,
        ]);

        return response([
            'title'     => 'Success!',
            'message'   => 'Update User',
            'type'      => 'success'
        ], 200);
    }

    /**
     * Remove the specified resource from storage.
     *
     * @param \App\Models\User $user
     * @return \Illuminate\Http\Response
     */
    public function destroy(User $user)
    {
        if ($user) {
            if($user->profile) if(File::exists(public_path("storages/$user->profile"))) File::delete(public_path("storages/$user->profile"));
            $user->delete();
            return response([
                'title'     => 'Success!',
                'message'   => 'Delete User',
                'type'      => 'success',
            ], 200);
        } else {
            return response([
                'title'     => 'Failed!',
                'message'   => 'Delete User',
                'type'      => 'error',
            ], 200);
        }
    }

    /**
     * Export a resource from storage to Excel.
     *
     * @param  \Illuminate\Http\Request $request
     * @return \Maatwebsite\Excel\Facades\Excel
     */
    public function export(Request $request)
    {
        return Excel::download(new UsersExport($request->all()), 'users-' . Carbon::now() . '.xls', Excels::XLS);
    }

    /**
     * Import Excel a resource to storage.
     *
     * @param  \Illuminate\Http\Request $request
     * @return \Illuminate\Http\Response
     */
    public function import(Request $request)
    {
        $validation = Validator::make($request->all(),[
            'excel' => 'required|mimes:xlx,xls,xlsx'
        ])->fails();

        if ($validation)
            return back()->withErrors([
                'title'     => 'Failed!',
                'message'   => 'Import Families',
                'type'      => 'error',
            ]);

        Excel::import(new UsersImport, $request->file('excel'));
        return back()->withErrors([
            'title'     => 'Success!',
            'message'   => 'Import Families',
            'type'      => 'success'
        ]);
    }

    /**
     * Validate a data from request.
     *
     * @param  array $data
     * @param  \App\Models\User $user
     * @param  boolean $update
     * @return boolean
     */
    public function validation(array $data, User $user = null, $update = false) {
        if (!$update) {
            $credentials = [
                'id_family' => 'required|exists:families,id_family|unique:users,id_family',
                'email'     => 'required|email|unique:users',
                'phone'     => 'required|unique:users|max:15',
                'username'  => 'required|unique:users',
            ];

        } else {
            $credentials = [
                'id_family' => 'required|exists:families,id_family|unique:users,id_family,' . $user->id_user . ',id_user',
                'email'     => 'required|email|unique:users,email,' . $user->id_user . ',id_user',
                'phone'     => 'required|unique:users,phone,' . $user->id_user . ',id_user',
                'username'  => 'required|unique:users,username,' . $user->id_user . ',id_user',
            ];

        }

        if(isset($data['password']))
            $credentials = array_merge($credentials, [
                'password'   => 'min:5',
            ]);

        $validation = Validator::make($data ,array_merge(
            $credentials,
            [
                'role'      => 'required|integer',
            ]
        ));

        return !($validation->fails() || (!$user && $update));
    }
}
```
</details>

<details>
<summary>Create Hash & Encryption</summary>

Here is how I create encryption and hash, my goal is to maintain data integrity and security, here I make it simple because the data stored is not very sensitive data
```php
<?php
namespace App\Helpers;

use Illuminate\Support\Facades\Crypt as Encrypt;
use Illuminate\Contracts\Encryption\DecryptException;
use Illuminate\Support\Facades\Config;

class Crypt extends Encrypt {
    
    /**
     * Encrypt the given parameter with added complexity.
     *
     * @param string $param
     * @return string
     */
    public static function encryption($param) {
        $salt = openssl_random_pseudo_bytes(16);
        return base64_encode($salt . Encrypt::encryptString($salt . $param));
    }

    /**
     * Decrypt the given parameter with added complexity.
     *
     * @param string $param
     * @return string
     * @throws DecryptException
     */
    public static function decryption($param) {
        try {
            $decoded = base64_decode($param);
            $salt = substr($decoded, 0, 16);
            $encrypted = substr($decoded, 16);
            return substr(Encrypt::decryptString($encrypted), 16);
        } catch (DecryptException $e) {
            throw new DecryptException("Failed to decrypt the parameter.");
        }
    }

    /**
     * Hash the given parameter with added complexity.
     *
     * @param string $param
     * @return string
     */
    public static function crypt($param) {
        return base64_encode(strrev(hash('sha256', (openssl_random_pseudo_bytes(16) . env('APP_KEY') . $param))));
    }

    /**
     * Decrypt a collection of items with specified keys.
     *
     * @param array|object $collection
     * @param array $keys
     * @return array|object
     */
    public static function decrypt($collection, array $keys) {
        if (isset($collection[0])) {
            $isArray = is_array($collection[0]);
            foreach ($collection as $index => $item) {
                foreach ($keys as $key) {
                    if ($isArray) {
                        $item[$key] = self::decryption($item[$key]);
                    } else {
                        $item->{$key} = self::decryption($item->{$key});
                    }
                }
                $collection[$index] = $item;
            }
        } else {
            $isArray = is_array($collection);
            foreach ($keys as $key) {
                if ($isArray) {
                    $collection[$key] = self::decryption($collection[$key]);
                } else {
                    $collection->{$key} = self::decryption($collection->{$key});
                }
            }
        }

        return $collection;
    }

    /**
     * Find a specific item in the decrypted collection by key and value.
     *
     * @param array|object $collection
     * @param string $key
     * @param string $value
     * @return mixed
     */
    public static function find($collection, $key, $value) {
        return self::decrypt($collection, [$key])->firstWhere($key, $value) ?: false;
    }
}
```
</details>
