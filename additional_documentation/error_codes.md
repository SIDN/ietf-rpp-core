    epp_code_map = {
        "1000": ResultCode.COMMAND_COMPLETED_SUCCESSFULLY, -> 200 OK
        "1001": ResultCode.COMMAND_COMPLETED_ACTION_PENDING, -> 202 Accepted
        "1300": ResultCode.COMMAND_COMPLETED_NO_MESSAGES, -> 200 OK
        "1301": ResultCode.COMMAND_COMPLETED_ACK_TO_DEQUEUE, -> 200 OK
        "1500": ResultCode.COMMAND_COMPLETED_ENDING_SESSION, -> N/A

    "2000": ResultCode.UNKNOWN_COMMAND, -> 400 Bad Request
        "2001": ResultCode.COMMAND_SYNTAX_ERROR, -> 400 Bad Request
        "2002": ResultCode.COMMAND_USE_ERROR, -> 400 Bad Request
        "2003": ResultCode.REQUIRED_PARAMETER_MISSING, -> 400 Bad Request
        "2004": ResultCode.PARAMETER_VALUE_RANGE_ERROR, -> 400 Bad Request
        "2005": ResultCode.PARAMETER_VALUE_SYNTAX_ERROR, -> 400 Bad Request
        "2100": ResultCode.UNIMPLEMENTED_PROTOCOL_VERSION,  -> 501 Not Implemented
        "2101": ResultCode.UNIMPLEMENTED_COMMAND, -> 501 Not Implemented
        "2102": ResultCode.UNIMPLEMENTED_OPTION, -> 501 Not Implemented
        "2103": ResultCode.UNIMPLEMENTED_EXTENSION, -> 501 Not Implemented
        "2104": ResultCode.BILLING_FAILURE, -> 400 Bad Request
        "2105": ResultCode.OBJECT_NOT_ELIGIBLE_FOR_RENEWAL, -> 400 Bad Request
        "2106": ResultCode.OBJECT_NOT_ELIGIBLE_FOR_TRANSFER, -> 400 Bad Request
        "2200": ResultCode.AUTHENTICATION_ERROR, -> 403 Forbidden
        "2201": ResultCode.AUTHORIZATION_ERROR, -> 403 Forbidden
        "2202": ResultCode.INVALID_AUTHORIZATION_INFORMATION, -> 403 Forbidden
        "2300": ResultCode.OBJECT_PENDING_TRANSFER, -> 400 Bad Request
        "2301": ResultCode.OBJECT_NOT_PENDING_TRANSFER, -> 400 Bad Request
        "2302": ResultCode.OBJECT_EXISTS, -> 409 Conflict
        "2303": ResultCode.OBJECT_DOES_NOT_EXIST, -> 404 Not Found
        "2304": ResultCode.OBJECT_STATUS_PROHIBITS_OPERATION, -> 400 Bad Request
        "2305": ResultCode.OBJECT_ASSOCIATION_PROHIBITS_OPERATION, -> 400 Bad Request
        "2306": ResultCode.PARAMETER_VALUE_POLICY_ERROR, -> 400 Bad Request
        "2307": ResultCode.UNIMPLEMENTED_OBJECT_SERVICE, -> 400 Bad Request
        "2308": ResultCode.DATA_MANAGEMENT_POLICY_VIOLATION, -> 400 Bad Request
        "2400": ResultCode.COMMAND_FAILED, -> 500 Internal Server Error
        "2500": ResultCode.COMMAND_FAILED_SERVER_CLOSING_CONNECTION, -> n/a
        "2501": ResultCode.AUTHENTICATION_ERROR_SERVER_CLOSING_CONNECTION, -> n/a
        "2502": ResultCode.SESSION_LIMIT_EXCEEDED_SERVER_CLOSING_CONNECTION, -> n/a
    }
