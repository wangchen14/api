# api

userAuthController

<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

use App\Http\Requests;
use Validator;
use Illuminate\Http\Response;


class UserAuthController extends Controller
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
    }

    /**
     * Show the form for creating a new resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function create()
    {
        //
    }

    /**
     * Store a newly created resource in storage.
     *
     * @param  \Illuminate\Http\Request  $request
     * @return \Illuminate\Http\Response
     */
    public function store(Request $request)
    {
                $credentials = $request->all();

                $validator = Validator::make($request->all(), [
                 'mobile' => 'required|unique |max:255',
                'email' => 'required',
                'password'=> 'required'
                    ]);

                
                if ($validator->fails()) {

                        $status= false;
                        $message='you validation failed';

                    return response($status);
                            
                    }

                 else{

                    $newUser = \App\User::create([
                    
                 
                    'mobile' => $request->input('mobile'),

                    'email' => $request->input('email'),
                    'password' => bcrypt($request->input('password'),

                    ]);


                    $token= md5(uniqid($credentials, true));

                    $user = new User;

                    $user->authtoken = $token;

                    $user->save();

                    $status = 'true';

                    return response($token, $status);



            }

           




        }

    /**
     * Display the specified resource.
     *
     * @param  int  $id
     * @return \Illuminate\Http\Response
     */
    public function show($id)
    {
        //
    }

    /**
     * Show the form for editing the specified resource.
     *
     * @param  int  $id
     * @return \Illuminate\Http\Response
     */
    public function edit($id)
    {
        //
    }

    /**
     * Update the specified resource in storage.
     *
     * @param  \Illuminate\Http\Request  $request
     * @param  int  $id
     * @return \Illuminate\Http\Response
     */
    public function update(Request $request, $id)
    {
        //
    }

    /**
     * Remove the specified resource from storage.
     *
     * @param  int  $id
     * @return \Illuminate\Http\Response
     */
    public function destroy($id)
    {
        //
    }
}
