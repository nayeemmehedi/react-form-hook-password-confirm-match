# react-form-hook-password-confirm-match

    "use client";
    
    import React from "react";
    import { useForm } from "react-hook-form";
    import "../../globals.css";
    import { yupResolver } from "@hookform/resolvers/yup";
    import * as yup from "yup";
    import "./signup.css";
    
    function Signup() {
      const schema = yup
        .object({
          firstName: yup.string().required("this is required"),
          email: yup.string().required("this is required"),
          password: yup.string().required("this is required"),
          confirmPassword: yup
            .string()
            .oneOf([yup.ref("password"), null], "Passwords must match")
            .required("this is required"),
        })
        .required();
    
      const {
        register,
        formState: { errors },
        handleSubmit,
      } = useForm({
        resolver: yupResolver(schema),
      });
    
      console.log(errors);
    
      const onSubmit = (data) => console.log(data);
    
      return (
        <div className="h-screen bg-slate-950 ">
          <div className=" text-red-500">
            <form onSubmit={handleSubmit(onSubmit)}>
              <label>Name</label>
              <input
                className="border-4 border-red-700 focus:border-green-800"
                {...register("firstName")}
              />
    
              {errors.firstName?.type === "required" && (
                <p role="alert">{errors.firstName.message}</p>
              )}
    
              <label>Email</label>
    
              <input {...register("email")} />
    
              {errors.email && (
                <p className="text-red-700" role="alert">
                  {errors.email.message?.split(",")[0]}
                </p>
              )}
    
              <label>Password</label>
    
              <input type="password" {...register("password")} />
    
              {errors.password && (
                <p className="text-red-700" role="alert">
                  {errors.password.message?.split(",")[0]}
                </p>
              )}
    
              <label>Confirm Password</label>
    
              <input type="password" {...register("confirmPassword")} />
    
              {errors.confirmPassword && (
                <p className="text-red-700" role="alert">
                  {errors.confirmPassword.message?.split(",")[0]}
                </p>
              )}
    
              <input type="submit" />
            </form>
          </div>
        </div>
      );
    }
    
    export default Signup;
